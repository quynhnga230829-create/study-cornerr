<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Góc Học Tập Thông Minh - StudySpace</title>
    <!-- Tailwind CSS và FontAwesome Icons -->
    <script src="https://jsdelivr.net"></script>
    <link rel="stylesheet" href="https://cloudflare.com">
    <style>
        /* Tùy chỉnh thanh cuộn mượt mà */
        html { scroll-behavior: smooth; }
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }
        .dark ::-webkit-scrollbar-track { background: #1f2937; }
        ::-webkit-scrollbar-thumb { background: #888; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #555; }
    </style>
</head>
<body class="bg-gray-50 text-gray-800 dark:bg-gray-900 dark:text-gray-100 transition-colors duration-300 min-h-screen flex flex-col">

    <!-- Thanh điều hướng (Navbar) -->
    <nav class="sticky top-0 z-50 bg-white/80 dark:bg-gray-800/80 backdrop-blur-md shadow-sm border-b border-gray-100 dark:border-gray-700">
        <div class="max-w-6xl mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-2 font-bold text-xl text-indigo-600 dark:text-indigo-400">
                <i class="fa-solid fa-graduation-cap text-2xl"></i>
                <span>StudySpace</span>
            </div>
            <div class="hidden md:flex space-x-6 font-medium text-sm">
                <a href="#tips" class="hover:text-indigo-600 transition">Mẹo Học Tập</a>
                <a href="#methods" class="hover:text-indigo-600 transition">Phương Pháp</a>
                <a href="#pomodoro" class="hover:text-indigo-600 transition">Đồng Hồ Pomodoro</a>
                <a href="#todo" class="hover:text-indigo-600 transition">Việc Cần Làm</a>
                <a href="#schedule" class="hover:text-indigo-600 transition">Kế Hoạch Ngày</a>
            </div>
            <button id="theme-toggle" class="p-2 rounded-full hover:bg-gray-100 dark:hover:bg-gray-700 transition" aria-label="Đổi giao diện">
                <i class="fa-solid fa-moon text-lg block dark:hidden"></i>
                <i class="fa-solid fa-sun text-lg hidden dark:block text-yellow-400"></i>
            </button>
        </div>
    </nav>

    <!-- Nội dung chính -->
    <main class="max-w-6xl mx-auto px-4 py-8 flex-grow space-y-12 w-full">
        
        <!-- Khu vực Tiện ích: Pomodoro + Todo List -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
            
            <!-- ⏰ Tính năng 3: Đồng hồ Pomodoro 25 phút -->
            <section id="pomodoro" class="lg:col-span-5 bg-white dark:bg-gray-800 p-6 rounded-2xl shadow-sm border border-gray-100 dark:border-gray-700 text-center">
                <h2 class="text-xl font-bold mb-4 flex items-center justify-center gap-2">
                    <span>⏰</span> Đồng Hồ Pomodoro
                </h2>
                <div class="flex justify-center space-x-2 mb-6 text-xs font-semibold">
                    <button id="btn-pomo" class="px-3 py-1.5 rounded-full bg-indigo-100 dark:bg-indigo-900 text-indigo-700 dark:text-indigo-300">Pomodoro (25m)</button>
                    <button id="btn-short" class="px-3 py-1.5 rounded-full bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300">Nghỉ ngắn (5m)</button>
                </div>
                <!-- Vòng quay thời gian -->
                <div class="w-48 h-48 mx-auto my-6 rounded-full border-4 border-indigo-500 dark:border-indigo-400 flex flex-col items-center justify-center bg-gray-50 dark:bg-gray-900/50 shadow-inner relative">
                    <span id="timer-display" class="text-4xl font-extrabold tracking-wider tabular-nums text-gray-900 dark:text-white">25:00</span>
                    <span id="timer-status" class="text-xs text-gray-500 dark:text-gray-400 mt-1 uppercase tracking-widest font-medium">Tập trung</span>
                </div>
                <!-- Nút điều khiển -->
                <div class="flex justify-center space-x-4 mt-6">
                    <button id="btn-start" class="px-6 py-2 bg-indigo-600 hover:bg-indigo-700 text-white rounded-xl font-medium shadow-md transition flex items-center gap-2">
                        <i class="fa-solid fa-play"></i> Bắt đầu
                    </button>
                    <button id="btn-reset" class="px-6 py-2 bg-gray-200 dark:bg-gray-700 hover:bg-gray-300 dark:hover:bg-gray-600 rounded-xl font-medium transition flex items-center gap-2">
                        <i class="fa-solid fa-rotate-left"></i> Đặt lại
                    </button>
                </div>
                <audio id="alert-sound" src="https://mixkit.co" preload="auto"></audio>
            </section>

            <!-- 📝 Tính năng 4: Danh sách công việc cần hoàn thành (Todo) -->
            <section id="todo" class="lg:col-span-7 bg-white dark:bg-gray-800 p-6 rounded-2xl shadow-sm border border-gray-100 dark:border-gray-700 flex flex-col h-full min-h-[350px]">
                <h2 class="text-xl font-bold mb-4 flex items-center gap-2">
                    <span>📝</span> Nhiệm Vụ Cần Hoàn Thành
                </h2>
                <form id="todo-form" class="flex gap-2 mb-4">
                    <input type="text" id="todo-input" placeholder="Thêm công việc hoặc bài tập mới..." required class="flex-grow px-4 py-2 rounded-xl border border-gray-300 dark:border-gray-600 bg-transparent focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm">
                    <button type="submit" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-white rounded-xl font-medium transition text-sm whitespace-nowrap">
                        <i class="fa-solid fa-plus"></i> Thêm
                    </button>
                </form>
                <div class="overflow-y-auto max-h-[220px] flex-grow pr-1">
                    <ul id="todo-list" class="space-y-2">
                        <!-- Danh sách hiển thị động bằng JS -->
                    </ul>
                </div>
            </section>
        </div>

        <!-- 📅 Tính năng 5: Kế hoạch học tập mỗi ngày -->
        <section id="schedule" class="bg-white dark:bg-gray-800 p-6 rounded-2xl shadow-sm border border-gray-100 dark:border-gray-700">
            <h2 class="text-xl font-bold mb-6 flex items-center gap-2">
                <span>📅</span> Thời Khóa Biểu & Kế Hoạch Hôm Nay
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="p-4 bg-indigo-50/50 dark:bg-indigo-950/20 rounded-xl border border-indigo-100/50 dark:border-indigo-900/50">
                    <div class="flex items-center gap-2 text-indigo-600 dark:text-indigo-400 font-bold mb-2">
                        <span class="text-sm px-2 py-0.5 bg-indigo-100 dark:bg-indigo-900 rounded">Sáng</span>
                        <span>08:00 - 11:30</span>
                    </div>
                    <p class="text-sm text-gray-600 dark:text-gray-300">Tập trung học các môn tư duy nặng, đọc tài liệu mới, nghiên cứu bài khó hoặc làm bài tập lớn.</p>
                </div>
                <div class="p-4 bg-amber-50/50 dark:bg-amber-950/20 rounded-xl border border-amber-100/50 dark:border-amber-900/50">
                    <div class="flex items-center gap-2 text-amber-600 dark:text-amber-400 font-bold mb-2">
                        <span class="text-sm px-2 py-0.5 bg-amber-100 dark:bg-amber-900 rounded">Chiều</span>
                        <span>14:00 - 17:30</span>
                    </div>
                    <p class="text-sm text-gray-600 dark:text-gray-300">Luyện đề, làm bài tập thực hành, họp nhóm hoặc hoàn thành các đầu việc ngắn hạn trong danh sách.</p>
                </div>
                <div class="p-4 bg-emerald-50/50 dark:bg-emerald-950/20 rounded-xl border border-emerald-100/50 dark:border-emerald-900/50">
                    <div class="flex items-center gap-2 text-emerald-600 dark:text-emerald-400 font-bold mb-2">
                        <span class="text-sm px-2 py-0.5 bg-emerald-100 dark:bg-emerald-900 rounded">Tối</span>
                        <span>20:00 - 22:30</span>
                    </div>
                    <p class="text-sm text-gray-600 dark:text-gray-300">Ôn tập lại kiến thức cũ trong ngày bằng Flashcard, ghi chép tóm tắt và lên kế hoạch cho ngày mai.</p>
                </div>
            </div>
        </section>

        <!-- 📚 Tính năng 1: Mẹo học tập hiệu quả -->
        <section id="tips" class="space-y-4">
            <h2 class="text-2xl font-bold flex items-center gap-2">
                <span>📚</span> Mẹo Học Tập Hiệu Quả Cao
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
                <div class="bg-white dark:bg-gray-800 p-5 rounded-xl shadow-sm border border-gray-100 dark:border-gray-700 hover:-translate-y-1 transition duration-300">
                    <div class="text-2xl mb-2">💡</div>
                    <h3 class="font-bold text-base mb-1">Không gian tối giản</h3>
                    <p class="text-xs text-gray-500 dark:text-gray-400">Dọn dẹp mặt bàn học sạch sẽ. Cất điện thoại ở xa tầm mắt để tránh cám dỗ từ thông báo MXH.</p>
                </div>
                <div class="bg-white dark:bg-gray-800 p-5 rounded-xl shadow-sm border border-gray-100 dark:border-gray-700 hover:-translate-y-1 transition duration-300">
                    <div class="text-2xl mb-2">💧</div>
                    <h3 class="font-bold text-base mb-1">Cung cấp đủ nước</h3>
                    <p class="text-xs text-gray-500 dark:text-gray-400">Thiếu nước làm não bộ giảm tốc độ xử lý thông tin. Luôn để sẵn một ly nước lọc trên bàn.</p>
                </div>
