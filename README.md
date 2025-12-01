# monndaisyu
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>個別授業管理</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }
        
        header {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        h1 {
            color: #f5576c;
            font-size: 2.5em;
        }
        
        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
        }
        
        .tab {
            padding: 15px 30px;
            background: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1.1em;
            color: #666;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .tab.active {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            font-weight: bold;
        }
        
        .tab:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.15);
        }
        
        .card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        .card h2 {
            color: #333;
            margin-bottom: 20px;
            border-bottom: 3px solid #f5576c;
            padding-bottom: 10px;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1em;
            transition: all 0.3s;
            font-weight: bold;
        }
        
        .btn-primary {
            background: #f5576c;
            color: white;
        }
        
        .btn-primary:hover {
            background: #e04556;
        }
        
        .btn-success {
            background: #51cf66;
            color: white;
        }
        
        .btn-success:hover {
            background: #40c057;
        }
        
        .btn-danger {
            background: #ff6b6b;
            color: white;
            padding: 8px 16px;
        }
        
        .btn-secondary {
            background: #868e96;
            color: white;
        }
        
        .lesson-item {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 5px solid #f5576c;
        }
        
        .lesson-item.past {
            opacity: 0.6;
            border-left-color: #adb5bd;
        }
        
        .lesson-header {
            display: flex;
            justify-content: space-between;
            align-items: start;
            margin-bottom: 15px;
        }
        
        .lesson-title {
            font-size: 1.3em;
            font-weight: bold;
            color: #333;
            margin-bottom: 8px;
        }
        
        .lesson-info {
            display: flex;
            gap: 20px;
            color: #666;
            font-size: 0.9em;
            flex-wrap: wrap;
        }
        
        .lesson-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        
        .homework-section {
            background: #fff3cd;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
        }
        
        .homework-section h4 {
            color: #856404;
            margin-bottom: 10px;
        }
        
        .homework-item {
            padding: 8px;
            background: white;
            border-radius: 5px;
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .homework-item.done {
            opacity: 0.5;
            text-decoration: line-through;
        }
        
        .memo-section {
            background: #e7f5ff;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
        }
        
        .memo-section h4 {
            color: #1971c2;
            margin-bottom: 10px;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }
        
        .modal.show {
            display: flex;
        }
        
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            max-width: 600px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #333;
        }
        
        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            font-size: 1em;
            font-family: inherit;
        }
        
        .form-group textarea {
            resize: vertical;
            min-height: 80px;
        }
        
        .modal-buttons {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }
        
        .modal-buttons button {
            flex: 1;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .stat-card {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 25px;
            border-radius: 15px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 3em;
            font-weight: bold;
        }
        
        .stat-label {
            font-size: 1.1em;
            opacity: 0.9;
            margin-top: 5px;
        }
        
        .calendar {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
        }
        
        .calendar-day {
            aspect-ratio: 1;
            padding: 10px;
            border-radius: 10px;
            text-align: center;
            background: #f8f9fa;
            border: 2px solid #e9ecef;
            cursor: pointer;
        }
        
        .calendar-day.has-lesson {
            background: #ffe3e8;
            border-color: #f5576c;
            font-weight: bold;
        }
        
        .calendar-header {
            font-weight: bold;
            color: #666;
            padding: 10px;
        }
        
        .empty-state {
            text-align: center;
            padding: 60px;
            color: #999;
            font-size: 1.2em;
        }
        
        .checkbox-input {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
        
        .notification-badge {
            background: #51cf66;
            color: white;
            padding: 3px 8px;
            border-radius: 12px;
            font-size: 0.8em;
            font-weight: bold;
            margin-left: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>📚 個別授業管理</h1>
        </header>

        <div class="tabs">
            <button class="tab active" onclick="switchTab('today')">📅 今日</button>
            <button class="tab" onclick="switchTab('week')">📆 今週</button>
            <button class="tab" onclick="switchTab('calendar')">🗓️ カレンダー</button>
            <button class="tab" onclick="switchTab('stats')">📊 統計</button>
        </div>

        <button class="btn btn-primary" onclick="showAddLessonModal()" style="width: 100%; padding: 15px; margin-bottom: 20px; font-size: 1.2em;">
            ➕ 授業を追加
        </button>

        <div id="content"></div>
    </div>

    <!-- 授業追加モーダル -->
    <div id="addLessonModal" class="modal">
        <div class="modal-content">
            <h2>授業を追加</h2>
            
            <div class="form-group">
                <label>教科</label>
                <input type="text" id="lessonSubject" placeholder="例: 数学">
            </div>
            
            <div class="form-group">
                <label>先生名</label>
                <input type="text" id="lessonTeacher" placeholder="例: 山田先生">
            </div>
            
            <div class="form-group">
                <label>日時</label>
                <input type="datetime-local" id="lessonDateTime">
            </div>
            
            <div class="form-group">
                <label>時間（分）</label>
                <input type="number" id="lessonDuration" value="60" min="15" step="15">
            </div>
            
            <div class="form-group">
                <label>場所（任意）</label>
                <input type="text" id="lessonLocation" placeholder="例: A教室">
            </div>
            
            <div class="form-group">
                <label>通知（授業の何分前？）</label>
                <select id="lessonNotification">
                    <option value="0">通知しない</option>
                    <option value="15" selected>15分前</option>
                    <option value="30">30分前</option>
                    <option value="60">1時間前</option>
                </select>
            </div>
            
            <div class="modal-buttons">
                <button class="btn btn-secondary" onclick="closeModal('addLessonModal')">キャンセル</button>
                <button class="btn btn-success" onclick="addLesson()">追加</button>
            </div>
        </div>
    </div>

    <!-- 宿題追加モーダル -->
    <div id="addHomeworkModal" class="modal">
        <div class="modal-content">
            <h2>宿題を追加</h2>
            
            <div class="form-group">
                <label>宿題内容</label>
                <textarea id="homeworkContent" placeholder="例: 問題集p.20-25"></textarea>
            </div>
            
            <div class="modal-buttons">
                <button class="btn btn-secondary" onclick="closeModal('addHomeworkModal')">キャンセル</button>
                <button class="btn btn-success" onclick="addHomework()">追加</button>
            </div>
        </div>
    </div>

    <!-- メモ追加モーダル -->
    <div id="addMemoModal" class="modal">
        <div class="modal-content">
            <h2>授業メモを追加</h2>
            
            <div class="form-group">
                <label>今日習ったこと</label>
                <textarea id="memoContent" placeholder="例: 二次関数の基礎、グラフの書き方" style="min-height: 150px;"></textarea>
            </div>
            
            <div class="modal-buttons">
                <button class="btn btn-secondary" onclick="closeModal('addMemoModal')">キャンセル</button>
                <button class="btn btn-success" onclick="addMemo()">保存</button>
            </div>
        </div>
    </div>

    <script>
        let lessons = [];
        let currentTab = 'today';
        let currentLessonId = null;

        function loadData() {
            try {
                const data = localStorage.getItem('tutoring-lessons');
                if (data) {
                    lessons = JSON.parse(data);
                }
            } catch (error) {
                console.error('読み込みエラー:', error);
            }
            renderContent();
        }

        function saveData() {
            try {
                localStorage.setItem('tutoring-lessons', JSON.stringify(lessons));
                renderContent();
            } catch (error) {
                console.error('保存エラー:', error);
                alert('保存に失敗しました');
            }
        }

        function switchTab(tab) {
            currentTab = tab;
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            event.target.classList.add('active');
            renderContent();
        }

        function renderContent() {
            const content = document.getElementById('content');
            
            if (currentTab === 'today') {
                renderTodayLessons(content);
            } else if (currentTab === 'week') {
                renderWeekLessons(content);
            } else if (currentTab === 'calendar') {
                renderCalendar(content);
            } else if (currentTab === 'stats') {
                renderStats(content);
            }
        }

        function renderTodayLessons(content) {
            const today = new Date();
            today.setHours(0, 0, 0, 0);
            const tomorrow = new Date(today);
            tomorrow.setDate(tomorrow.getDate() + 1);

            const todayLessons = lessons.filter(l => {
                const lessonDate = new Date(l.datetime);
                return lessonDate >= today && lessonDate < tomorrow;
            }).sort((a, b) => new Date(a.datetime) - new Date(b.datetime));

            content.innerHTML = `
                <div class="card">
                    <h2>📅 今日の授業</h2>
                    ${todayLessons.length === 0 
                        ? '<div class="empty-state">今日の授業はありません</div>'
                        : todayLessons.map(lesson => renderLessonItem(lesson)).join('')
                    }
                </div>
            `;
        }

        function renderWeekLessons(content) {
            const today = new Date();
            today.setHours(0, 0, 0, 0);
            const nextWeek = new Date(today);
            nextWeek.setDate(nextWeek.getDate() + 7);

            const weekLessons = lessons.filter(l => {
                const lessonDate = new Date(l.datetime);
                return lessonDate >= today && lessonDate < nextWeek;
            }).sort((a, b) => new Date(a.datetime) - new Date(b.datetime));

            content.innerHTML = `
                <div class="card">
                    <h2>📆 今週の授業</h2>
                    ${weekLessons.length === 0 
                        ? '<div class="empty-state">今週の授業はありません</div>'
                        : weekLessons.map(lesson => renderLessonItem(lesson)).join('')
                    }
                </div>
            `;
        }

        function renderLessonItem(lesson) {
            const lessonDate = new Date(lesson.datetime);
            const now = new Date();
            const isPast = lessonDate < now;
            const dateStr = lessonDate.toLocaleString('ja-JP');

            const homeworkCount = lesson.homework ? lesson.homework.filter(h => !h.done).length : 0;

            return `
                <div class="lesson-item ${isPast ? 'past' : ''}">
                    <div class="lesson-header">
                        <div>
                            <div class="lesson-title">
                                ${lesson.subject}
                                ${homeworkCount > 0 ? `<span class="notification-badge">${homeworkCount}件の宿題</span>` : ''}
                            </div>
                            <div class="lesson-info">
                                <span>👨‍🏫 ${lesson.teacher}</span>
                                <span>🕐 ${dateStr}</span>
                                <span>⏱️ ${lesson.duration}分</span>
                                ${lesson.location ? `<span>📍 ${lesson.location}</span>` : ''}
                            </div>
                        </div>
                        <div class="lesson-buttons">
                            <button class="btn btn-primary" onclick="openHomeworkModal(${lesson.id})">宿題</button>
                            <button class="btn btn-success" onclick="openMemoModal(${lesson.id})">メモ</button>
                            <button class="btn btn-danger" onclick="deleteLesson(${lesson.id})">削除</button>
                        </div>
                    </div>
                    
                    ${lesson.homework && lesson.homework.length > 0 ? `
                        <div class="homework-section">
                            <h4>📝 宿題</h4>
                            ${lesson.homework.map((hw, idx) => `
                                <div class="homework-item ${hw.done ? 'done' : ''}">
                                    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
                                        <input type="checkbox" class="checkbox-input" ${hw.done ? 'checked' : ''} 
                                               onchange="toggleHomework(${lesson.id}, ${idx})">
                                        <span>${hw.content}</span>
                                    </label>
                                </div>
                            `).join('')}
                        </div>
                    ` : ''}
                    
                    ${lesson.memo ? `
                        <div class="memo-section">
                            <h4>📓 授業メモ</h4>
                            <div style="white-space: pre-wrap;">${lesson.memo}</div>
                        </div>
                    ` : ''}
                </div>
            `;
        }

        function renderCalendar(content) {
            const now = new Date();
            const year = now.getFullYear();
            const month = now.getMonth();
            const firstDay = new Date(year, month, 1);
            const lastDay = new Date(year, month + 1, 0);
            const daysInMonth = lastDay.getDate();
            const startingDayOfWeek = firstDay.getDay();

            const days = [];
            for (let i = 0; i < startingDayOfWeek; i++) {
                days.push(null);
            }
            for (let i = 1; i <= daysInMonth; i++) {
                days.push(i);
            }

            const dayNames = ['日', '月', '火', '水', '木', '金', '土'];

            content.innerHTML = `
                <div class="card">
                    <h2 style="text-align: center;">${year}年 ${month + 1}月</h2>
                    <div class="calendar">
                        ${dayNames.map(name => `<div class="calendar-header">${name}</div>`).join('')}
                        ${days.map(day => {
                            if (!day) return '<div></div>';
                            
                            const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                            const dayLessons = lessons.filter(l => {
                                const lessonDate = new Date(l.datetime);
                                return lessonDate.toISOString().split('T')[0] === dateStr;
                            });

                            return `
                                <div class="calendar-day ${dayLessons.length > 0 ? 'has-lesson' : ''}">
                                    <div style="font-weight: bold;">${day}</div>
                                    ${dayLessons.length > 0 ? `<div style="color: #f5576c; font-size: 0.8em;">${dayLessons.length}件</div>` : ''}
                                </div>
                            `;
                        }).join('')}
                    </div>
                </div>
            `;
        }

        function renderStats(content) {
            const now = new Date();
            const thisMonth = lessons.filter(l => {
                const lessonDate = new Date(l.datetime);
                return lessonDate.getMonth() === now.getMonth() && 
                       lessonDate.getFullYear() === now.getFullYear();
            }).length;

            const totalHomework = lessons.reduce((sum, l) => sum + (l.homework ? l.homework.length : 0), 0);
            const doneHomework = lessons.reduce((sum, l) => 
                sum + (l.homework ? l.homework.filter(h => h.done).length : 0), 0);
            const totalLessons = lessons.length;

            content.innerHTML = `
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-label">今月の授業数</div>
                        <div class="stat-value">${thisMonth}</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">総授業数</div>
                        <div class="stat-value">${totalLessons}</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">宿題完了率</div>
                        <div class="stat-value">${totalHomework > 0 ? Math.round(doneHomework / totalHomework * 100) : 0}%</div>
                    </div>
                </div>
                
                <div class="card">
                    <h2>📚 全ての授業</h2>
                    ${lessons.length === 0 
                        ? '<div class="empty-state">授業がありません</div>'
                        : lessons.sort((a, b) => new Date(b.datetime) - new Date(a.datetime))
                            .map(lesson => renderLessonItem(lesson)).join('')
                    }
                </div>
            `;
        }

        function showAddLessonModal() {
            document.getElementById('addLessonModal').classList.add('show');
            document.getElementById('lessonSubject').value = '';
            document.getElementById('lessonTeacher').value = '';
            document.getElementById('lessonDateTime').value = '';
            document.getElementById('lessonDuration').value = '60';
            document.getElementById('lessonLocation').value = '';
            document.getElementById('lessonSubject').focus();
        }

        function closeModal(id) {
            document.getElementById(id).classList.remove('show');
        }

        function addLesson() {
            const subject = document.getElementById('lessonSubject').value.trim();
            const teacher = document.getElementById('lessonTeacher').value.trim();
            const datetime = document.getElementById('lessonDateTime').value;
            const duration = parseInt(document.getElementById('lessonDuration').value);
            const location = document.getElementById('lessonLocation').value.trim();
            const notification = parseInt(document.getElementById('lessonNotification').value);

            if (!subject || !teacher || !datetime) {
                alert('教科、先生名、日時を入力してください');
                return;
            }

            const lesson = {
                id: Date.now(),
                subject,
                teacher,
                datetime,
                duration,
                location,
                notification,
                homework: [],
                memo: ''
            };

            lessons.push(lesson);
            saveData();
            closeModal('addLessonModal');

            if (notification > 0) {
                sendNotificationToApp(lesson);
            }
        }

        function sendNotificationToApp(lesson) {
            const lessonDate = new Date(lesson.datetime);
            const notifDate = new Date(lessonDate.getTime() - lesson.notification * 60000);

            const request = {
                title: `授業: ${lesson.subject}`,
                message: `${lesson.teacher}の授業が${lesson.notification}分後に始まります`,
                datetime: notifDate.toISOString().slice(0, 16),
                source: '個別授業アプリ'
            };

            localStorage.setItem('notification-request', JSON.stringify(request));
            alert('通知が設定されました！');
        }

        function deleteLesson(id) {
            if (!confirm('この授業を削除しますか？')) return;
            lessons = lessons.filter(l => l.id !== id);
            saveData();
        }

        function openHomeworkModal(lessonId) {
            currentLessonId = lessonId;
            document.getElementById('addHomeworkModal').classList.add('show');
            document.getElementById('homeworkContent').value = '';
            document.getElementById('homeworkContent').focus();
        }

        function addHomework() {
            const content = document.getElementById('homeworkContent').value.trim();
            if (!content) {
                alert('宿題内容を入力してください');
                return;
            }

            lessons = lessons.map(l => {
                if (l.id === currentLessonId) {
                    return {
                        ...l,
                        homework: [...(l.homework || []), { content, done: false }]
                    };
                }
                return l;
            });

            saveData();
            closeModal('addHomeworkModal');
        }

        function toggleHomework(lessonId, homeworkIndex) {
            lessons = lessons.map(l => {
                if (l.id === lessonId) {
                    const newHomework = [...l.homework];
                    newHomework[homeworkIndex].done = !newHomework[homeworkIndex].done;
                    return { ...l, homework: newHomework };
                }
                return l;
            });
            saveData();
        }

        function openMemoModal(lessonId) {
            currentLessonId = lessonId;
            const lesson = lessons.find(l => l.id === lessonId);
            document.getElementById('addMemoModal').classList.add('show');
            document.getElementById('memoContent').value = lesson.memo || '';
            document.getElementById('memoContent').focus();
        }

        function addMemo() {
            const content = document.getElementById('memoContent').value.trim();

            lessons = lessons.map(l => {
                if (l.id === currentLessonId) {
                    return { ...l, memo: content };
                }
                return l;
            });

            saveData();
            closeModal('addMemoModal');
        }

        loadData();
    </script>
</body>
</html>
