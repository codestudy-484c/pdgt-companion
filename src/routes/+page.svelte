<script lang="ts">
    /* [2단계] 표정 상태 관리*/
    // let currentFace = $state('ᓀ‸ᓂ ');
    // let isActive = $state(false);

    /* [3단계] 센서 권한 및 리스너 */

    /* [4단계] 스트레스 수치 및 타이머 */

    // 임시 변수 (1단계 레이아웃 확인용)
    let displayFace = 'ᓀ‸ᓂ ';

    /* [5단계] PiP & Canvas 관련 함수 정의 구역 */
    const requestPermission = () => {
        // Button for step 3 sensor permission asker logic
        alert("Under Construction");
    }
    
    const togglePiP = () => {
        // Button for step 5 PiP conversion logic
        alert("Under Construction");
    }
</script>

<main>
    <section class="face-display">
        <div class="face-text">
            {displayFace}
        </div>
    </section>
    
    <section class="controls">
        <button class="btn primary" onclick={requestPermission}>
            Connect to Device
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
</style>
