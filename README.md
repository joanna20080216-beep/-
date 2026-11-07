<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>亞洲大學匿名霸凌系統 | Asia University Anonymous Bullying System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        au: {
                            blue: '#1e3a8a',
                            light: '#3b82f6',
                            red: '#dc2626',
                            dark: '#0f172a'
                        }
                    }
                }
            }
        }
    </script>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col font-sans">

    <!-- 隱蔽保護色遮罩 (預設隱藏) -->
    <div id="panic-screen" class="fixed inset-0 bg-white z-50 hidden flex flex-col justify-between p-6">
        <div class="border-b pb-4 flex justify-between items-center">
            <h1 class="text-2xl font-bold text-blue-900"><i class="fas fa-graduation-cap mr-2"></i>亞洲大學數位學習系統</h1>
            <div class="text-sm text-gray-500">系統時間：<span id="panic-time"></span> | 歡迎您，學生</div>
        </div>
        <div class="max-w-4xl mx-auto w-full space-y-4">
            <div class="bg-blue-50 border border-blue-200 p-4 rounded-lg">
                <h3 class="font-bold text-blue-900 mb-1">【公告】115學年度第一學期期中教學意見調查通知</h3>
                <p class="text-sm text-gray-600">各位同學好，請於規定期間內完成本學期各課程之線上教學意見調查，以維護自身權益。</p>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div class="border p-4 rounded-lg bg-gray-50">
                    <h4 class="font-semibold text-gray-700 mb-2">我的課程清單</h4>
                    <ul class="text-sm space-y-2 text-blue-600">
                        <li><a href="#" class="hover:underline">▸ 人工智慧與倫理導論 (資工系)</a></li>
                        <li><a href="#" class="hover:underline">▸ 心理學概論 (心理系)</a></li>
                        <li><a href="#" class="hover:underline">▸ 大學國文與現代文學 (通識)</a></li>
                    </ul>
                </div>
                <div class="border p-4 rounded-lg bg-gray-50">
                    <h4 class="font-semibold text-gray-700 mb-2">近期作業繳交</h4>
                    <p class="text-sm text-gray-500">目前尚無未繳交作業。</p>
                </div>
            </div>
        </div>
        <div class="text-center text-xs text-gray-400 border-t pt-4 flex justify-between items-center">
            <span>Asia University e-Learning Platform © 2026</span>
            <button onclick="togglePanic()" class="text-xs bg-gray-200 hover:bg-gray-300 text-gray-700 px-3 py-1 rounded">點擊此處或按 ESC 返回系統</button>
        </div>
    </div>

    <!-- 頂部導覽列 -->
    <header class="bg-au-blue text-white shadow-md sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 py-3 flex flex-wrap justify-between items-center">
            <div class="flex items-center space-x-3 cursor-pointer" onclick="switchTab('home')">
                <div class="bg-white text-au-blue p-2 rounded-lg font-bold text-lg"><i class="fas fa-shield-alt"></i></div>
                <div>
                    <h1 class="font-bold text-lg leading-tight" data-i18n="nav_title">亞洲大學匿名霸凌系統</h1>
                    <p class="text-xs text-blue-200" data-i18n="nav_subtitle">Asia University Anonymous Bullying System (繞過校方行政)</p>
                </div>
            </div>

            <!-- 功能按鈕與語系 -->
            <div class="flex items-center space-x-3 mt-2 sm:mt-0">
                <select id="lang-select" onchange="changeLanguage(this.value)" class="bg-blue-900 text-white text-xs px-2 py-1.5 rounded border border-blue-700 focus:outline-none">
                    <option value="zh">繁體中文</option>
                    <option value="en">English</option>
                    <option value="ja">日本語</option>
                </select>

                <button onclick="switchTab('home')" class="text-xs px-3 py-1.5 bg-blue-800 hover:bg-blue-700 rounded transition" data-i18n="tab_home">首頁</button>
                <button onclick="switchTab('report')" class="text-xs px-3 py-1.5 bg-au-red hover:bg-red-700 font-semibold rounded transition shadow" data-i18n="tab_report"><i class="fas fa-bullhorn mr-1"></i>匿名通報</button>
                <button onclick="switchTab('counseling')" class="text-xs px-3 py-1.5 bg-emerald-600 hover:bg-emerald-500 font-semibold rounded transition shadow" data-i18n="tab_counseling"><i class="fas fa-heartbeat mr-1"></i>L101 諮商預約</button>
                <button onclick="switchTab('track')" class="text-xs px-3 py-1.5 bg-blue-800 hover:bg-blue-700 rounded transition" data-i18n="tab_track">案件進度</button>
                <button onclick="switchTab('admin')" class="text-xs px-3 py-1.5 bg-slate-700 hover:bg-slate-600 rounded transition" data-i18n="tab_admin"><i class="fas fa-user-shield mr-1"></i>管理者後台</button>

                <!-- 緊急掩護按鈕 -->
                <button onclick="togglePanic()" class="bg-gray-800 hover:bg-gray-900 text-yellow-300 px-3 py-1.5 rounded text-xs border border-yellow-500/50 shadow flex items-center font-bold" title="按 Esc 鍵即可快速切換">
                    <i class="fas fa-eye-slash mr-1"></i><span data-i18n="panic_btn">快速隱蔽 (Esc)</span>
                </button>
            </div>
        </div>
    </header>

    <!-- 主內容區 -->
    <main class="flex-grow max-w-7xl mx-auto px-4 py-8 w-full">

        <!-- 首頁標籤 -->
        <div id="section-home" class="space-y-6">
            <div class="bg-gradient-to-r from-blue-900 to-indigo-900 text-white p-8 rounded-2xl shadow-xl relative overflow-hidden">
                <div class="absolute right-0 bottom-0 opacity-10 text-9xl transform translate-x-10 translate-y-10">
                    <i class="fas fa-shield-alt"></i>
                </div>
                <div class="max-w-2xl relative z-10">
                    <span class="bg-red-600 text-white text-xs px-3 py-1 rounded-full font-semibold uppercase tracking-wider" data-i18n="hero_badge">獨立匿名保護機制</span>
                    <h2 class="text-3xl font-bold mt-3 mb-2" data-i18n="hero_title">勇敢說不，不必獨自承受</h2>
                    <p class="text-blue-100 text-sm leading-relaxed mb-6" data-i18n="hero_desc">
                        本系統專為亞洲大學學生設計。若您在校園中遭受霸凌、不當對待或權力壓迫，您可以透過本平台直接通報與對接諮商輔導組（L101），全程嚴格保密，<strong>完全繞過系所老師與校內行政通報系統</strong>。
                    </p>
                    <div class="flex flex-wrap gap-4">
                        <button onclick="switchTab('report')" class="bg-au-red hover:bg-red-700 text-white px-6 py-3 rounded-lg font-bold text-sm shadow-lg transition flex items-center">
                            <i class="fas fa-exclamation-triangle mr-2"></i><span data-i18n="btn_start_report">立即匿名通報</span>
                        </button>
                        <button onclick="switchTab('counseling')" class="bg-emerald-600 hover:bg-emerald-500 text-white px-6 py-3 rounded-lg font-bold text-sm shadow-lg transition flex items-center">
                            <i class="fas fa-hands-helping mr-2"></i><span data-i18n="btn_start_counseling">預約 L101 心理諮商</span>
                        </button>
                    </div>
                </div>
            </div>

            <!-- 特色卡片 -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-100">
                    <div class="w-12 h-12 bg-blue-100 text-au-blue rounded-lg flex items-center justify-center text-xl mb-4">
                        <i class="fas fa-user-secret"></i>
                    </div>
                    <h3 class="font-bold text-lg mb-2" data-i18n="card1_title">100% 獨立保密</h3>
                    <p class="text-sm text-slate-600" data-i18n="card1_desc">不經過系辦、導師或系主任，資料直接加密送至專業心輔中心與外部支援組織，保護您的隱私免受二次傷害。</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-100">
                    <div class="w-12 h-12 bg-emerald-100 text-emerald-600 rounded-lg flex items-center justify-center text-xl mb-4">
                        <i class="fas fa-map-marked-alt"></i>
                    </div>
                    <h3 class="font-bold text-lg mb-2" data-i18n="card2_title">亞大 L101 直接連動</h3>
                    <p class="text-sm text-slate-600" data-i18n="card2_desc">與亞洲大學諮商中心（L101）緊密對接，專人專線提供心理支持與法律/權益諮詢，協助您走出陰霾。</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-100">
                    <div class="w-12 h-12 bg-amber-100 text-amber-600 rounded-lg flex items-center justify-center text-xl mb-4">
                        <i class="fas fa-shield-virus"></i>
                    </div>
                    <h3 class="font-bold text-lg mb-2" data-i18n="card3_title">快速隱蔽防護</h3>
                    <p class="text-sm text-slate-600" data-i18n="card3_desc">隨時點擊右上角或按下 ESC 鍵，畫面將立即偽裝成亞大數位學習系統，保護您的螢幕安全。</p>
                </div>
            </div>

            <!-- 校外支援管道資訊 -->
            <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-200">
                <h3 class="font-bold text-lg text-slate-900 mb-4 flex items-center">
                    <i class="fas fa-phone-alt text-au-red mr-2"></i><span data-i18n="ext_resources_title">校內外外部求助專線與資源</span>
                </h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
                    <div class="p-4 bg-slate-50 rounded-lg border">
                        <h4 class="font-bold text-blue-900 mb-1">亞洲大學 諮商與健康中心</h4>
                        <p class="text-slate-600 mb-1">📍 辦公地點：<strong>L101</strong></p>
                        <p class="text-slate-600">📞 諮商專線：<strong>04-23323456</strong> 轉分機 <span class="text-blue-700 font-semibold">6265、6267、6268、6269、1745、1763、1768</span></p>
                    </div>
                    <div 
