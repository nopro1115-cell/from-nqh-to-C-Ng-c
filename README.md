<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>20/11 - Gửi Cô Ngọc</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@400;500;600;700&family=Cormorant+Garamond:ital,wght@0,600;0,700;1,600&family=Dancing+Script:wght@600;700&display=swap" rel="stylesheet">

    <style>
        /* Thiết lập cơ bản an toàn, chống tràn ngang và chống nhảy layout */
        *, *::before, *::after {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        html, body {
            margin: 0;
            padding: 0;
            width: 100%;
            min-height: 100vh;
            min-height: 100dvh;
            overflow-x: hidden;
            overflow-y: auto;
            font-family: 'Be Vietnam Pro', sans-serif;
            background: radial-gradient(circle at 50% 30%, #3b0d1b 0%, #1d060e 58%, #0c0206 100%);
            color: #fffbeb;
        }

        .font-display-serif {
            font-family: 'Cormorant Garamond', serif;
        }

        .font-script {
            font-family: 'Dancing Script', cursive;
        }

        /* Ánh sáng nền ấm áp chuyển động rất chậm, không gây giật */
        .ambient-glow {
            position: fixed;
            border-radius: 9999px;
            filter: blur(80px);
            opacity: 0.28;
            pointer-events: none;
            z-index: 0;
            animation: slowGlow 16s ease-in-out infinite alternate;
        }

        @keyframes slowGlow {
            0% {
                transform: translate3d(0, 0, 0) scale(1);
            }
            100% {
                transform: translate3d(24px, -18px, 0) scale(1.08);
            }
        }

        /* Bó hoa chuyển động nhẹ nhàng, không giật */
        @keyframes gentleFloat {
            0%, 100% {
                transform: translate3d(0, 0, 0);
            }
            50% {
                transform: translate3d(0, -6px, 0);
            }
        }

        .bouquet-box {
            animation: gentleFloat 5.5s ease-in-out infinite;
            transition: opacity 0.55s ease, transform 0.55s ease;
        }

        .bouquet-box.is-hidden {
            opacity: 0;
            transform: translate3d(0, 14px, 0) scale(0.96);
            pointer-events: none;
        }

        /* Bao lì xì nằm cố định ngay giữa bó hoa, không giật khi chạm */
        .envelope-btn {
            position: absolute;
            top: 52%;
            left: 50%;
            transform: translate(-50%, -50%);
            transition: opacity 0.4s ease, transform 0.35s ease;
            cursor: pointer;
            outline: none;
        }

        .envelope-btn:focus-visible {
            box-shadow: 0 0 0 3px rgba(253, 224, 71, 0.75);
        }

        .envelope-btn.is-opened {
            opacity: 0;
            transform: translate(-50%, -58%) scale(0.95);
            pointer-events: none;
        }

        /* Chữ chuỗi mở đầu 3 -> 2 -> 1 -> HAPPY TEACHERS' DAY -> 20/11 */
        .intro-step {
            opacity: 0;
            transform: translate3d(0, 10px, 0) scale(0.96);
            transition: opacity 0.35s ease, transform 0.4s ease;
        }

        .intro-step.is-active {
            opacity: 1;
            transform: translate3d(0, 0, 0) scale(1);
        }

        .intro-step.is-leaving {
            opacity: 0;
            transform: translate3d(0, -10px, 0) scale(1.03);
        }

        /* Khung thiệp cố định cân đối giữa màn hình, không nhảy khi gõ chữ */
        .card-shell {
            transition: opacity 0.55s ease, transform 0.55s ease;
        }

        .card-shell.is-hidden {
            opacity: 0;
            transform: translate3d(0, 16px, 0);
            pointer-events: none;
        }

        .card-shell.is-visible {
            opacity: 1;
            transform: translate3d(0, 0, 0);
            pointer-events: auto;
        }

        .card-frame {
            background: linear-gradient(160deg, rgba(76, 12, 27, 0.96) 0%, rgba(38, 6, 14, 0.98) 100%);
            box-shadow:
                0 24px 60px rgba(0, 0, 0, 0.7),
                0 0 0 1px rgba(251, 191, 36, 0.35),
                0 0 36px rgba(245, 158, 11, 0.16);
        }

        .card-paper {
            background: linear-gradient(180deg, #fffdf7 0%, #fef5dc 100%);
            box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.9), inset 0 0 18px rgba(180, 83, 9, 0.08);
        }

        /* Chiều cao cố định cho vùng lời chúc để chữ chạy không làm giật thiệp */
        .wish-box {
            min-height: 176px;
        }

        @media (min-width: 640px) {
            .wish-box {
                min-height: 152px;
            }
        }
    </style>
</head>
<body class="relative flex flex-col items-center justify-center min-h-screen px-4 py-6">

    <!-- Ánh sáng nền nhẹ nhàng -->
    <div class="ambient-glow w-72 h-72 sm:w-96 sm:h-96 bg-rose-700 top-[-40px] left-[-40px]"></div>
    <div class="ambient-glow w-80 h-80 sm:w-[420px] sm:h-[420px] bg-amber-600 bottom-[-60px] right-[-40px]" style="animation-delay: -7s;"></div>

    <!-- Nút bật/tắt nhạc gọn ở góc trên bên phải -->
    <header class="fixed top-3.5 right-3.5 sm:top-5 sm:right-5 z-50">
        <button id="musicToggleBtn" type="button" aria-label="Bật hoặc tắt nhạc nền Người Gieo Mầm Xanh"
            class="inline-flex items-center gap-2 px-3.5 py-2 sm:px-4 sm:py-2.5 rounded-full bg-stone-950/75 hover:bg-stone-900 text-amber-200 border border-amber-400/45 shadow-lg backdrop-blur-md text-xs sm:text-sm font-medium transition-colors cursor-pointer">
            <span id="musicStatusIcon" aria-hidden="true">♪</span>
            <span id="musicStatusLabel">Nhạc: Tắt</span>
        </button>
    </header>

    <!-- Canvas hiệu ứng cánh hoa rơi & ánh kim nhẹ nhàng -->
    <canvas id="celebrationCanvas" class="fixed inset-0 w-full h-full pointer-events-none z-30"></canvas>

    <!-- MÀN HÌNH 1: BÓ HOA & BAO LÌ XÌ Ở TRUNG TÂM -->
    <main id="bouquetScene" class="relative z-20 w-full max-w-[360px] sm:max-w-[430px] flex items-center justify-center my-auto">
        <div id="bouquetBox" class="bouquet-box relative w-full aspect-[4/4.4] flex items-center justify-center">

            <!-- Vầng sáng dịu phía sau bó hoa -->
            <div class="absolute inset-10 rounded-full bg-amber-400/15 blur-2xl pointer-events-none"></div>

            <!-- Bó hoa SVG nghệ thuật -->
            <svg viewBox="0 0 420 460" class="w-full h-full drop-shadow-[0_18px_28px_rgba(0,0,0,0.55)]" aria-hidden="true">
                <defs>
                    <linearGradient id="wrapOuter" x1="0%" y1="0%" x2="100%" y2="100%">
                        <stop offset="0%" stop-color="#ffe4e6"/>
                        <stop offset="55%" stop-color="#fecdd3"/>
                        <stop offset="100%" stop-color="#fda4af"/>
                    </linearGradient>
                    <linearGradient id="wrapInner" x1="0%" y1="0%" x2="0%" y2="100%">
                        <stop offset="0%" stop-color="#fffbeb"/>
                        <stop offset="100%" stop-color="#fde68a"/>
                    </linearGradient>
                    <linearGradient id="goldTrim" x1="0%" y1="0%" x2="100%" y2="0%">
                        <stop offset="0%" stop-color="#d97706"/>
                        <stop offset="50%" stop-color="#fef08a"/>
                        <stop offset="100%" stop-color="#b45309"/>
                    </linearGradient>
                    <radialGradient id="roseRed" cx="38%" cy="32%" r="68%">
                        <stop offset="0%" stop-color="#fb7185"/>
                        <stop offset="55%" stop-color="#e11d48"/>
                        <stop offset="100%" stop-color="#881337"/>
                    </radialGradient>
                    <radialGradient id="rosePink" cx="38%" cy="32%" r="68%">
                        <stop offset="0%" stop-color="#fff1f2"/>
                        <stop offset="55%" stop-color="#f472b6"/>
                        <stop offset="100%" stop-color="#be185d"/>
                    </radialGradient>
                    <radialGradient id="sunflowerPetal" cx="50%" cy="50%" r="50%">
                        <stop offset="0%" stop-color="#fef9c3"/>
                        <stop offset="65%" stop-color="#facc15"/>
                        <stop offset="100%" stop-color="#ca8a04"/>
                    </radialGradient>
                    <linearGradient id="ribbonGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                        <stop offset="0%" stop-color="#ef4444"/>
                        <stop offset="60%" stop-color="#b91c1c"/>
                        <stop offset="100%" stop-color="#7f1d1d"/>
                    </linearGradient>
                </defs>

                <!-- Giấy gói lớp sau -->
                <path d="M210 390 L62 156 Q118 88 210 112 Q302 88 358 156 Z" fill="url(#wrapOuter)" stroke="#fb7185" stroke-width="1.5"/>
                <path d="M210 390 L86 166 Q132 112 210 128 Q288 112 334 166 Z" fill="url(#wrapInner)" opacity="0.85"/>
                <path d="M210 390 L42 194 Q74 132 136 142 Z" fill="#ffe4e6" stroke="#fda4af" stroke-width="1.5"/>
                <path d="M210 390 L378 194 Q346 132 284 142 Z" fill="#ffe4e6" stroke="#fda4af" stroke-width="1.5"/>
                <path d="M68 160 Q124 100 210 120 Q296 100 352 160" fill="none" stroke="url(#goldTrim)" stroke-width="2" stroke-dasharray="6 4"/>

                <!-- Lá xanh -->
                <g>
                    <path d="M118 170 Q72 126 54 152 Q82 180 118 170 Z" fill="#15803d"/>
                    <path d="M98 206 Q50 184 46 210 Q76 226 98 206 Z" fill="#166534"/>
                    <path d="M302 170 Q348 126 366 152 Q338 180 302 170 Z" fill="#15803d"/>
                    <path d="M322 206 Q370 184 374 210 Q344 226 322 206 Z" fill="#166534"/>
                    <path d="M164 122 Q142 70 168 62 Q190 92 164 122 Z" fill="#22c55e"/>
                    <path d="M256 122 Q278 70 252 62 Q230 92 256 122 Z" fill="#22c55e"/>
                    <path d="M210 110 Q208 56 228 60 Q234 90 210 110 Z" fill="#15803d"/>
                </g>

                <!-- Hoa hướng dương trái -->
                <g transform="translate(128, 144)">
                    <g fill="url(#sunflowerPetal)" stroke="#d97706" stroke-width="0.7">
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(0)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(30)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(60)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(90)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(120)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(150)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(180)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(210)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(240)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(270)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(300)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(330)"/>
                    </g>
                    <circle cx="0" cy="0" r="14.5" fill="#78350f"/>
                    <circle cx="0" cy="0" r="10.5" fill="#451a03" stroke="#f59e0b" stroke-width="1.3" stroke-dasharray="2 2"/>
                </g>

                <!-- Hoa hướng dương phải -->
                <g transform="translate(292, 146) scale(0.95)">
                    <g fill="url(#sunflowerPetal)" stroke="#d97706" stroke-width="0.7">
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(15)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(45)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(75)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(105)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(135)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(165)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(195)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(225)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(255)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(285)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(315)"/>
                        <ellipse cx="0" cy="-28" rx="6.8" ry="16.5" transform="rotate(345)"/>
                    </g>
                    <circle cx="0" cy="0" r="14.5" fill="#78350f"/>
                    <circle cx="0" cy="0" r="10.5" fill="#451a03" stroke="#f59e0b" stroke-width="1.3" stroke-dasharray="2 2"/>
                </g>

                <!-- Hoa hồng đỏ trung tâm -->
                <g transform="translate(210, 114) scale(1.12)">
                    <circle cx="0" cy="0" r="32" fill="url(#roseRed)"/>
                    <path d="M-23 -6 C-27 -23, 0 -31, 15 -19 C29 -10, 25 19, 4 23 C-17 27, -27 10, -19 -6" fill="none" stroke="#ffe4e6" stroke-width="1.5" opacity="0.82"/>
                    <path d="M-13 -4 C-15 -15, 2 -19, 10 -11 C17 -4, 13 11, 2 13 C-9 15, -15 6, -10 -4" fill="none" stroke="#fecdd3" stroke-width="1.7" opacity="0.9"/>
                    <path d="M-5 -2 C-6 -8, 2 -10, 6 -5 C9 0, 6 7, 0 7 C-5 7, -7 2, -4 -2" fill="none" stroke="#fff1f2" stroke-width="1.7"/>
                </g>

                <!-- Hoa hồng phấn hai bên -->
                <g transform="translate(94, 198) scale(0.95)">
                    <circle cx="0" cy="0" r="27" fill="url(#rosePink)"/>
                    <path d="M-19 -5 C-21 -19, 0 -25, 13 -15 C23 -8, 19 15, 3 19 C-14 21, -21 8, -15 -5" fill="none" stroke="#fff1f2" stroke-width="1.5" opacity="0.85"/>
                </g>
                <g transform="translate(326, 198) scale(0.95)">
                    <circle cx="0" cy="0" r="27" fill="url(#rosePink)"/>
                    <path d="M-19 -5 C-21 -19, 0 -25, 13 -15 C23 -8, 19 15, 3 19 C-14 21, -21 8, -15 -5" fill="none" stroke="#fff1f2" stroke-width="1.5" opacity="0.85"/>
                </g>

                <!-- Hoa baby nhỏ -->
                <g fill="#ffffff" stroke="#fde047" stroke-width="1">
                    <circle cx="170" cy="96" r="4.5"/><circle cx="181" cy="88" r="4"/><circle cx="163" cy="86" r="3.8"/>
                    <circle cx="250" cy="96" r="4.5"/><circle cx="259" cy="86" r="4"/><circle cx="239" cy="87" r="3.8"/>
                    <circle cx="86" cy="160" r="4.5"/><circle cx="334" cy="160" r="4.5"/>
                </g>

                <!-- Giấy gói lớp trước -->
                <path d="M168 334 L144 438 Q210 454 276 438 L252 334 Z" fill="url(#wrapOuter)" stroke="#fda4af" stroke-width="1.5"/>
                <path d="M60 214 L174 348 L225 348 L124 224 Q88 204 60 214 Z" fill="url(#wrapOuter)" stroke="#fb7185" stroke-width="1.5"/>
                <path d="M360 214 L246 348 L195 348 L296 224 Q332 204 360 214 Z" fill="url(#wrapOuter)" stroke="#fb7185" stroke-width="1.5"/>
                <path d="M65 218 L174 345" fill="none" stroke="url(#goldTrim)" stroke-width="2"/>
                <path d="M355 218 L246 345" fill="none" stroke="url(#goldTrim)" stroke-width="2"/>

                <!-- Nơ đỏ viền vàng -->
                <g transform="translate(210, 348)">
                    <path d="M-12 5 Q-35 56 -52 96 L-35 88 L-27 102 Q-12 56 -4 10 Z" fill="url(#ribbonGrad)"/>
                    <path d="M12 5 Q35 56 52 96 L35 88 L27 102 Q12 56 4 10 Z" fill="url(#ribbonGrad)"/>
                    <path d="M-8 0 C-56 -28, -70 22, -10 12 Z" fill="url(#ribbonGrad)" stroke="#fde68a" stroke-width="1.1"/>
                    <path d="M8 0 C56 -28, 70 22, 10 12 Z" fill="url(#ribbonGrad)" stroke="#fde68a" stroke-width="1.1"/>
                    <rect x="-12" y="-10" width="24" height="22" rx="6" fill="#991b1b" stroke="#fde047" stroke-width="1.8"/>
                </g>
            </svg>

            <!-- Bao lì xì đỏ viền vàng nổi bật ngay giữa bó hoa -->
            <button id="envelopeTrigger" type="button" aria-label="Mở bao lì xì chúc mừng 20/11"
                class="envelope-btn w-[112px] sm:w-[132px] h-[154px] sm:h-[180px] rounded-2xl bg-gradient-to-b from-red-600 via-red-700 to-rose-950 border-2 border-amber-300 shadow-[0_14px_30px_rgba(0,0,0,0.55),0_0_22px_rgba(251,191,36,0.35)] flex flex-col items-center justify-center overflow-hidden">

                <!-- Đường viền chỉ vàng bên trong -->
                <div class="absolute inset-2 rounded-xl border border-amber-300/60 pointer-events-none"></div>

                <!-- Nắp bao lì xì trang trí -->
                <svg viewBox="0 0 140 62" class="absolute top-0 left-0 w-full h-[54px] sm:h-[62px] pointer-events-none" aria-hidden="true">
                    <path d="M0 0 L140 0 L140 16 Q70 64 0 16 Z" fill="#991b1b" stroke="#fde047" stroke-width="2"/>
                </svg>

                <!-- Biểu tượng hoa mai/trái tim vàng ở giữa bao lì xì -->
                <div class="relative z-10 mt-6 w-12 h-12 sm:w-14 sm:h-14 rounded-full bg-gradient-to-br from-amber-200 via-amber-400 to-amber-600 p-0.5 shadow-md flex items-center justify-center">
                    <div class="w-full h-full rounded-full bg-red-900 border border-amber-200/80 flex items-center justify-center text-amber-200 text-lg sm:text-xl font-bold">
                        ✦
                    </div>
                </div>
            </button>
        </div>
    </main>

    <!-- MÀN HÌNH 2: CHUỖI ĐẾM NGƯỢC (3 -> 2 -> 1 -> HAPPY TEACHERS' DAY -> 20/11) -->
    <div id="introSequenceLayer" class="fixed inset-0 z-20 flex items-center justify-center px-4 text-center pointer-events-none hidden">
        <div id="introStepBox" class="intro-step max-w-2xl w-full"></div>
    </div>

    <!-- MÀN HÌNH 3: TẤM THIỆP CHÚC MỪNG CỐ ĐỊNH CÂN ĐỐI GIỮA MÀN HÌNH -->
    <section id="cardSection" class="card-shell is-hidden fixed inset-0 z-20 flex flex-col items-center justify-center px-4 py-6 overflow-y-auto hidden">
        <div class="w-full max-w-xl my-auto flex flex-col items-center">

            <!-- Khung thiệp chính -->
            <article class="card-frame w-full rounded-3xl border border-amber-400/70 p-2.5 sm:p-4">
                <div class="card-paper rounded-2xl border border-amber-500/45 px-5 py-6 sm:px-9 sm:py-8 text-stone-800">

                    <!-- Phần đầu thiệp: Kính gửi Cô Ngọc -->
                    <div class="text-center border-b border-amber-500/25 pb-3.5 mb-4">
                        <p class="text-[11px] sm:text-xs font-semibold tracking-[0.22em] uppercase text-amber-700 mb-1">
                            Ngày Nhà Giáo Việt Nam • 20/11
                        </p>
                        <h1 class="font-script text-3xl sm:text-4xl font-bold text-red-900">
                            Kính gửi: Cô Ngọc
                        </h1>
                    </div>

                    <!-- Khung nội dung lời chúc có chiều cao ổn định, không làm giật thiệp -->
                    <div class="wish-box flex items-center justify-center">
                        <p id="wishParagraph" class="w-full text-[15px] sm:text-[17px] leading-[1.8] text-stone-800 font-medium text-left sm:text-center"></p>
                    </div>

                    <!-- Dòng cuối thiệp bên phải: From N.Quốc.Hậu -->
                    <div class="mt-4 pt-3 border-t border-amber-500/20 flex items-center justify-between gap-2">
                        <button id="skipTypingBtn" type="button"
                            class="text-xs text-amber-800 hover:text-red-800 underline underline-offset-4 cursor-pointer">
                            Xem toàn bộ
                        </button>
                        <p class="font-script text-2xl sm:text-[28px] font-bold text-red-900 text-right">
                            From N.Quốc.Hậu
                        </p>
                    </div>
                </div>
            </article>

            <!-- Nút xem lại / mở lại thiệp gọn gàng phía dưới -->
            <div class="mt-4 flex items-center justify-center">
                <button id="replayCardBtn" type="button"
                    class="px-5 py-2.5 rounded-full bg-red-950/85 hover:bg-red-900 text-amber-200 border border-amber-400/55 shadow-lg text-xs sm:text-sm font-medium transition-colors cursor-pointer">
                    Mở lại thiệp
                </button>
            </div>
        </div>
    </section>

    <script>
        /**
         * Nội dung lời chúc cố định gửi cô Ngọc
         */
        const WISH_MESSAGE = "Em chúc cô Ngọc 20/11 thật nhiều sức khỏe và niềm vui ạ! Tuy giờ không còn học cô nữa nhưng em vẫn quý và nhớ những gì cô chỉ bảo hồi trước lắm. Chúc cô ngày nào đi dạy cũng vui và gặp nhiều học trò ngoan nha cô!";

        /**
         * Bộ phát nhạc nền "Người Gieo Mầm Xanh" (đoạn điệp khúc cao trào) bằng Web Audio API
         * Hoạt động tin cậy trên iOS/Android và desktop sau thao tác chạm/click.
         */
        class NguoiGieoMamXanhAudio {
            constructor() {
                this.audioCtx = null;
                this.isPlaying = false;
                this.timerId = null;
                this.noteIndex = 0;

                const NOTE = {
                    REST: 0,
                    F2: 87.31, G2: 98.00, A2: 110.00, Bb2: 116.54, C3: 130.81, D3: 146.83,
                    E3: 164.81, F3: 174.61, G3: 196.00, A3: 220.00, Bb3: 233.08, C4: 261.63,
                    D4: 293.66, E4: 329.63, F4: 349.23, G4: 392.00, A4: 440.00, Bb4: 466.16,
                    C5: 523.25, D5: 587.33, E5: 659.25, F5: 698.46, G5: 783.99, A5: 880.00
                };

                const CHORD = {
                    F:  [NOTE.F3, NOTE.A3, NOTE.C4, NOTE.E4],
                    C:  [NOTE.E3, NOTE.G3, NOTE.C4, NOTE.E4],
                    Dm: [NOTE.D3, NOTE.F3, NOTE.A3, NOTE.C4],
                    Bb: [NOTE.Bb2, NOTE.D3, NOTE.F3, NOTE.A3],
                    Gm: [NOTE.G2, NOTE.Bb2, NOTE.D3, NOTE.F3]
                };

                // Giai điệu điệp khúc cao trào: "Đời là những chuyến đi dài, gieo mầm xanh cho tương lai..."
                this.phrase = [
                    { m: NOTE.C5, b: NOTE.F2,  c: CHORD.F,  sec: 0.36 },
                    { m: NOTE.D5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.F5, b: 0,       c: null,     sec: 0.52 },
                    { m: NOTE.A5, b: NOTE.C3,  c: CHORD.C,  sec: 0.52 },
                    { m: NOTE.G5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.F5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.G5, b: NOTE.D3,  c: CHORD.Dm, sec: 0.72 },
                    { m: NOTE.REST, b: 0,     c: null,     sec: 0.18 },

                    { m: NOTE.C5, b: NOTE.Bb2, c: CHORD.Bb, sec: 0.36 },
                    { m: NOTE.D5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.F5, b: 0,       c: null,     sec: 0.52 },
                    { m: NOTE.G5, b: NOTE.C3,  c: CHORD.C,  sec: 0.52 },
                    { m: NOTE.F5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.D5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.C5, b: NOTE.F2,  c: CHORD.F,  sec: 0.78 },
                    { m: NOTE.REST, b: 0,     c: null,     sec: 0.22 },

                    { m: NOTE.A4, b: NOTE.D3,  c: CHORD.Dm, sec: 0.36 },
                    { m: NOTE.C5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.D5, b: 0,       c: null,     sec: 0.52 },
                    { m: NOTE.F5, b: NOTE.A2,  c: CHORD.F,  sec: 0.52 },
                    { m: NOTE.D5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.C5, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.D5, b: NOTE.Bb2, c: CHORD.Bb, sec: 0.72 },
                    { m: NOTE.REST, b: 0,     c: null,     sec: 0.18 },

                    { m: NOTE.G4, b: NOTE.G2,  c: CHORD.Gm, sec: 0.36 },
                    { m: NOTE.A4, b: 0,       c: null,     sec: 0.36 },
                    { m: NOTE.C5, b: 0,       c: null,     sec: 0.46 },
                    { m: NOTE.D5, b: NOTE.C3,  c: CHORD.C,  sec: 0.46 },
                    { m: NOTE.F5, b: 0,       c: null,     sec: 0.52 },
                    { m: NOTE.G5, b: 0,       c: null,     sec: 0.52 },
                    { m: NOTE.F5, b: NOTE.F2,  c: CHORD.F,  sec: 1.15 },
                    { m: NOTE.REST, b: 0,     c: null,     sec: 0.40 }
                ];
            }

            async unlock() {
                try {
                    if (!this.audioCtx) {
                        const AudioContextClass = window.AudioContext || window.webkitAudioContext;
                        if (!AudioContextClass) return false;
                        this.audioCtx = new AudioContextClass();
                    }
                    if (this.audioCtx.state === 'suspended') {
                        await this.audioCtx.resume();
                    }
                    return this.audioCtx.state === 'running';
                } catch (err) {
                    return false;
                }
            }

            playLead(freq, sec) {
                if (!this.audioCtx || !freq) return;
                const now = this.audioCtx.currentTime;

                const osc = this.audioCtx.createOscillator();
                const overtone = this.audioCtx.createOscillator();
                const gain = this.audioCtx.createGain();
                const overtoneGain = this.audioCtx.createGain();

                osc.type = 'sine';
                osc.frequency.setValueAtTime(freq, now);

                overtone.type = 'triangle';
                overtone.frequency.setValueAtTime(freq * 2, now);

                gain.gain.setValueAtTime(0.0008, now);
                gain.gain.linearRampToValueAtTime(0.095, now + 0.025);
                gain.gain.exponentialRampToValueAtTime(0.0007, now + sec * 1.75);

                overtoneGain.gain.setValueAtTime(0.0005, now);
                overtoneGain.gain.linearRampToValueAtTime(0.02, now + 0.015);
                overtoneGain.gain.exponentialRampToValueAtTime(0.0002, now + sec * 0.85);

                osc.connect(gain);
                overtone.connect(overtoneGain);
                overtoneGain.connect(gain);
                gain.connect(this.audioCtx.destination);

                osc.start(now);
                overtone.start(now);
                osc.stop(now + sec * 1.8);
                overtone.stop(now + sec * 1.8);
            }

            playPadChord(freqs) {
                if (!this.audioCtx || !Array.isArray(freqs)) return;
                const now = this.audioCtx.currentTime;

                freqs.forEach((f, idx) => {
                    const osc = this.audioCtx.createOscillator();
                    const gain = this.audioCtx.createGain();
                    const startAt = now + idx * 0.025;

                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(f, startAt);

                    gain.gain.setValueAtTime(0.0004, startAt);
                    gain.gain.linearRampToValueAtTime(0.018, startAt + 0.08);
                    gain.gain.exponentialRampToValueAtTime(0.0003, startAt + 1.35);

                    osc.connect(gain);
                    gain.connect(this.audioCtx.destination);
                    osc.start(startAt);
                    osc.stop(startAt + 1.4);
                });
            }

            playBassNote(freq) {
                if (!this.audioCtx || !freq) return;
                const now = this.audioCtx.currentTime;

                const osc = this.audioCtx.createOscillator();
                const gain = this.audioCtx.createGain();

                osc.type = 'sine';
                osc.frequency.setValueAtTime(freq, now);

                gain.gain.setValueAtTime(0.0008, now);
                gain.gain.linearRampToValueAtTime(0.055, now + 0.035);
                gain.gain.exponentialRampToValueAtTime(0.0005, now + 1.25);

                osc.connect(gain);
                gain.connect(this.audioCtx.destination);
                osc.start(now);
                osc.stop(now + 1.3);
            }

            updateUI() {
                const labelEl = document.getElementById('musicStatusLabel');
                const iconEl = document.getElementById('musicStatusIcon');
                if (this.isPlaying) {
                    labelEl.textContent = 'Nhạc: Bật';
                    iconEl.textContent = '♫';
                } else {
                    labelEl.textContent = 'Nhạc: Tắt';
                    iconEl.textContent = '♪';
                }
            }

            async start() {
                const ok = await this.unlock();
                if (!ok) {
                    this.updateUI();
                    return;
                }
                if (this.isPlaying) {
                    this.updateUI();
                    return;
                }
                this.isPlaying = true;
                this.updateUI();
                this.scheduleNext();
            }

            scheduleNext() {
                if (!this.isPlaying) return;
                const current = this.phrase[this.noteIndex % this.phrase.length];
                if (current.m) this.playLead(current.m, current.sec);
                if (current.b) this.playBassNote(current.b);
                if (current.c) this.playPadChord(current.c);
                this.noteIndex++;
                this.timerId = window.setTimeout(() => this.scheduleNext(), current.sec * 1000);
            }

            stop() {
                this.isPlaying = false;
                if (this.timerId !== null) {
                    clearTimeout(this.timerId);
                    this.timerId = null;
                }
                this.updateUI();
            }

            async toggle() {
                if (this.isPlaying) {
                    this.stop();
                } else {
                    await this.start();
                }
            }
        }

        const bgMusic = new NguoiGieoMamXanhAudio();

        /**
         * Hiệu ứng cánh hoa rơi nhẹ và ánh kim vừa phải sau khi mở thiệp,
         * giới hạn số lượng hạt để chạy mượt trên điện thoại.
         */
        const fxCanvas = document.getElementById('celebrationCanvas');
        const fxCtx = fxCanvas.getContext('2d');
        let fxParticles = [];
        let celebrationActive = false;

        function syncCanvasSize() {
            fxCanvas.width = window.innerWidth;
            fxCanvas.height = window.innerHeight;
        }
        window.addEventListener('resize', syncCanvasSize);
        syncCanvasSize();

        class SoftParticle {
            constructor(kind) {
                this.kind = kind; // 'petal' | 'sparkle'
                this.x = Math.random() * fxCanvas.width;
                this.y = -16;
                this.vy = kind === 'petal' ? 0.9 + Math.random() * 1.15 : 0.7 + Math.random() * 0.9;
                this.vx = (Math.random() - 0.5) * 0.7;
                this.phase = Math.random() * Math.PI * 2;
                this.angle = Math.random() * Math.PI * 2;
                this.spin = (Math.random() - 0.5) * 0.035;
                this.size = kind === 'petal' ? 6 + Math.random() * 5 : 2.2 + Math.random() * 2.2;
                this.alpha = kind === 'petal' ? 0.75 : 0.65;
                const petalColors = ['#fda4af', '#fecdd3', '#fb7185'];
                this.color = kind === 'petal'
                    ? petalColors[Math.floor(Math.random() * petalColors.length)]
                    : '#fde68a';
            }

            step() {
                this.phase += 0.025;
                this.x += this.vx + Math.sin(this.phase) * 0.65;
                this.y += this.vy;
                this.angle += this.spin;
                if (this.y > fxCanvas.height - 60) {
                    this.alpha -= 0.015;
                }
            }

            draw(c) {
                if (this.alpha <= 0) return;
                c.save();
                c.globalAlpha = Math.max(0, this.alpha);
                c.translate(this.x, this.y);
                c.rotate(this.angle);
                c.fillStyle = this.color;

                if (this.kind === 'petal') {
                    c.beginPath();
                    c.ellipse(0, 0, this.size * 0.65, this.size, 0, 0, Math.PI * 2);
                    c.fill();
                } else {
                    c.fillRect(-this.size / 2, -this.size / 2, this.size, this.size);
                }
                c.restore();
            }
        }

        function renderCelebrationLoop() {
            fxCtx.clearRect(0, 0, fxCanvas.width, fxCanvas.height);

            if (celebrationActive && fxParticles.length < 42) {
                if (Math.random() < 0.14) {
                    fxParticles.push(new SoftParticle('petal'));
                } else if (Math.random() < 0.08) {
                    fxParticles.push(new SoftParticle('sparkle'));
                }
            }

            for (let i = fxParticles.length - 1; i >= 0; i--) {
                const p = fxParticles[i];
                p.step();
                p.draw(fxCtx);
                if (p.alpha <= 0 || p.y > fxCanvas.height + 24) {
                    fxParticles.splice(i, 1);
                }
            }

            requestAnimationFrame(renderCelebrationLoop);
        }

        /**
         * Điều phối chuỗi mở thiệp có khóa 1 lần kích hoạt để tránh chạm nhầm làm nhảy/lặp
         */
        const envelopeTrigger = document.getElementById('envelopeTrigger');
        const bouquetBox = document.getElementById('bouquetBox');
        const bouquetScene = document.getElementById('bouquetScene');
        const introSequenceLayer = document.getElementById('introSequenceLayer');
        const introStepBox = document.getElementById('introStepBox');
        const cardSection = document.getElementById('cardSection');
        const wishParagraph = document.getElementById('wishParagraph');
        const skipTypingBtn = document.getElementById('skipTypingBtn');
        const replayCardBtn = document.getElementById('replayCardBtn');
        const musicToggleBtn = document.getElementById('musicToggleBtn');

        let sequenceLocked = false;
        let typingIntervalId = null;
        let sequenceToken = 0;

        function waitMs(ms) {
            return new Promise((resolve) => window.setTimeout(resolve, ms));
        }

        function clearTypewriter() {
            if (typingIntervalId !== null) {
                clearInterval(typingIntervalId);
                typingIntervalId = null;
            }
        }

        function showFullWishImmediately() {
            clearTypewriter();
            wishParagraph.textContent = WISH_MESSAGE;
            skipTypingBtn.classList.add('hidden');
        }

        function startSmoothTypewriter(token) {
            clearTypewriter();
            wishParagraph.textContent = '';
            skipTypingBtn.classList.remove('hidden');

            let cursor = 0;
            typingIntervalId = window.setInterval(() => {
                if (token !== sequenceToken) {
                    clearTypewriter();
                    return;
                }
                if (cursor < WISH_MESSAGE.length) {
                    wishParagraph.textContent += WISH_MESSAGE.charAt(cursor);
                    cursor++;
                } else {
                    clearTypewriter();
                    skipTypingBtn.classList.add('hidden');
                }
            }, 34);
        }

        async function runIntroStep(markup, holdDuration, token) {
            if (token !== sequenceToken) return;
            introStepBox.className = 'intro-step max-w-2xl w-full';
            introStepBox.innerHTML = markup;
            void introStepBox.offsetWidth;
            introStepBox.classList.add('is-active');

            await waitMs(holdDuration);
            if (token !== sequenceToken) return;

            introStepBox.classList.remove('is-active');
            introStepBox.classList.add('is-leaving');
            await waitMs(360);
        }

        async function handleOpenEnvelope() {
            if (sequenceLocked) return;
            sequenceLocked = true;
            const currentToken = ++sequenceToken;

            // Phát nhạc nền "Người Gieo Mầm Xanh" ngay khi chạm mở bao lì xì
            bgMusic.start();

            envelopeTrigger.disabled = true;
            envelopeTrigger.classList.add('is-opened');
            bouquetBox.classList.add('is-hidden');

            await waitMs(450);
            if (currentToken !== sequenceToken) return;

            bouquetScene.classList.add('hidden');
            introSequenceLayer.classList.remove('hidden');

            // Bước 1: Đếm ngược 3 -> 2 -> 1
            for (const num of ['3', '2', '1']) {
                await runIntroStep(
                    `<span class="font-display-serif text-7xl sm:text-8xl font-bold text-amber-200 tracking-wide">${num}</span>`,
                    750,
                    currentToken
                );
                if (currentToken !== sequenceToken) return;
            }

            // Bước 2: HAPPY TEACHERS' DAY
            await runIntroStep(
                `<p class="font-display-serif text-3xl sm:text-5xl font-bold tracking-[0.14em] text-amber-200 uppercase leading-snug">
                    HAPPY TEACHERS' DAY
                </p>`,
                1450,
                currentToken
            );
            if (currentToken !== sequenceToken) return;

            // Bước 3: 20 / 11
            await runIntroStep(
                `<p class="font-display-serif text-5xl sm:text-7xl font-bold tracking-[0.2em] text-amber-300">
                    20 / 11
                </p>`,
                1300,
                currentToken
            );
            if (currentToken !== sequenceToken) return;

            // Bước 4: Mở tấm thiệp cố định cân đối giữa màn hình
            introSequenceLayer.classList.add('hidden');
            introStepBox.innerHTML = '';

            celebrationActive = true;
            cardSection.classList.remove('hidden');
            void cardSection.offsetWidth;
            cardSection.classList.remove('is-hidden');
            cardSection.classList.add('is-visible');

            startSmoothTypewriter(currentToken);
        }

        function resetToStart() {
            sequenceToken++;
            sequenceLocked = false;
            clearTypewriter();
            celebrationActive = false;

            cardSection.classList.remove('is-visible');
            cardSection.classList.add('is-hidden');
            cardSection.classList.add('hidden');

            introSequenceLayer.classList.add('hidden');
            introStepBox.innerHTML = '';

            wishParagraph.textContent = '';
            skipTypingBtn.classList.remove('hidden');

            bouquetScene.classList.remove('hidden');
            envelopeTrigger.disabled = false;
            envelopeTrigger.classList.remove('is-opened');
            void bouquetBox.offsetWidth;
            bouquetBox.classList.remove('is-hidden');
        }

        envelopeTrigger.addEventListener('click', handleOpenEnvelope);
        skipTypingBtn.addEventListener('click', showFullWishImmediately);
        replayCardBtn.addEventListener('click', resetToStart);
        musicToggleBtn.addEventListener('click', () => {
            bgMusic.toggle();
        });

        window.addEventListener('load', () => {
            renderCelebrationLoop();
        });
    </script>
</body>
</html>
