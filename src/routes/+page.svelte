<script lang="ts">
    import { onMount } from 'svelte';

    // [step 2] constants of 7 faces
    const FACES = {
        IDLE     : 'ᓀ‸ᓂ ',
        QUESTION : 'ᓀ‸ᓂ?',
        SUPRISE  : 'ᓀ‸ᓂ!',
        ANNOYED  : 'ᓀ‸ᓂ@',
        ANGRY    : 'ᓀ‸ᓂ+',
        TROUBLE  : 'ᓀ‸ᓂ;',
        BLINK    : 'ㅡ‸ㅡ '
    };

    /* [2단계] 표정 상태 관리*/
    let currentFace = $state(FACES.IDLE);
    let isInteracting = $state(false);

    // let isActive = $state(false);

    /* [3단계] 센서 권한 및 리스너 */
    let isSensorActive = $state(false);
    let permissionError = $state('');

    /* [4단계] 스트레스 수치 및 타이머 */

    /* blinking */
    $effect(() => {
        let blinkTimeout: ReturnType<typeof setTimeout>;

        const scheduleBlink = () => {
            const nextBlinkDelay = Math.random() * 3000 + 2000;
            
            blinkTimeout= setTimeout(() => {
                if (!isInteracting) {
                    currentFace = FACES.BLINK;

                    setTimeout(() => {
                        if (!isInteracting) {
                            currentFace = FACES.IDLE;
                        }
                    }, 200);
                }

                scheduleBlink();
            }, nextBlinkDelay);
        };
        
        scheduleBlink();

        return () => {
            clearTimeout(blinkTimeout);
        };
    });
    
    /* [step 4] sensor data function */
    const handleMotion = (event: DeviceMotionEvent) => {
        if (!isSensorActive) return;

        // TODO: event.acceleration logic
        console.log(event.acceleration?.x, event.acceleration?.y);
    };

    /* [step 3] Sensor Permission asking for iOS */
    const requestPermission = async () => {
        try {
            permissionError = '';       // Error Message Init

            // Check for device run iOS/iPadOS 13+
            if (typeof (DeviceMotionEvent as any).requestPermission === 'function') {
                const permissionState = await (DeviceMotionEvent as any).requestPermission();
                
                if (permissionState === 'granted') {
                    window.addEventListener('devicemotion', handleMotion);
                    isSensorActive = true;
                } else {
                    permissionError = 'Sensor Access permission denied. Allow Safari\'s sensor access permission on System Settings.';
                }

            } else {
                // for Android/under iOS 13
                window.addEventListener('devicemotion', handleMotion);
                isSensorActive = true;
            }

        } catch (error) {
            console.error('Error occured while get permission:', error);
            permissionError = 'Cannot get permission: Check for HTTPS';
        }
    };
    
    /* [5단계] PiP & Canvas 관련 함수 정의 구역 */
    const togglePiP = () => {
        // Button for step 5 PiP conversion logic
        alert("Under Construction");
    }
</script>

<main>
    <section class="face-display">
        <div class="face-text">
            {currentFace}
        </div>
    </section>
    
    <section class="controls">

        {#if permissionError}
            <div class="error-msg">{permissionError}</div>
        {/if}

        <button class="btn primary" onclick={requestPermission} disabled={isSensorActive}>
            {isSensorActive ? 'Connected' : 'Connect to Device' }
        </button>

        <button class="btn secondary" onclick={togglePiP}>
            Go To Pop-up
        </button>
    </section>
</main>

<style>
    /* default */
    :global(body) {
        margin: 0;
        padding: 0;
        background-color: #f5ecd3;
        color: #5e5e5e;
        font-family: Menlo, 'Courier New', Courier, monospace;
        overflow: hidden;
        user-select: none;
        -webkit-touch-callout: none;
    }

    main {
        display: flex;
        flex-direction: column;
        width: 100%;
        height: 100dvh;
    }
    
    .face-display {
        flex: 1;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 5rem;
        font-weight: bold;
        transition: all 0.2s ease;
    }
    
    .face-text {
        /* optional */
        text-shadow: 2px 2px 4px rgba(0,0,0,0.65);
    }

    /* bottom Btns */
    .controls {
        padding: 2rem;
        display: flex;
        flex-direction: column;
        gap: 1rem;
        padding-bottom: calc(2rem + env(safe-area-inset-bottom));
    }

    .btn {
        border: none;
        border-radius: 16px;
        padding: 1.2rem;
        font-size: 1.1rem;
        font-weight: 600;
        cursor: pointer;
        transition: transform 0.1s active;
        font-family: inherit;
    }

    .btn:active {
        transform: scale(0.98);
    }

    .primary {
        background-color: #5e5e5e;
        color: #f5ecd3;
    }

    .secondary {
        background-color: rgba(94, 94, 94, 0.1);
        color: #5e5e5e;
        border: 1px solid rgba(94, 94, 94, 0.2);
    }

    /* error-message style */
    .error-msg {
        color: #e74c3c;
        font-size: 0.9rem;
        text-align: center;
        margin-bottom: 0.5rem;
        font-weight: 600;
    }

    /* disable button */
    .btn:disabled {
        background-color: #a0a0a0;
        cursor: not-allowed;
        transform: none;
    }
</style>
