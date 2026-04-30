<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>快手速刷工具 - 网站版</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft YaHei", sans-serif;
        }

        body {
            background: #121212;
            color: #fff;
            padding: 20px;
            min-height: 100vh;
        }

        .container {
            max-width: 600px;
            margin: 0 auto;
        }

        /* 头部 */
        .header {
            background: linear-gradient(135deg, #2b5876 0%, #4e4376 100%);
            border-radius: 12px;
            padding: 24px;
            text-align: center;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }

        .header h1 {
            font-size: 24px;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .header h1::before {
            content: '⚡';
        }

        .header p {
            font-size: 14px;
            opacity: 0.8;
        }

        /* 模块 */
        .module {
            background: #1e1e1e;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        }

        .module-title {
            font-size: 16px;
            color: #4fc3f7;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* 进程选择 */
        .process-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .process-item {
            padding: 14px;
            background: #2d2d2d;
            border: 2px solid transparent;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 15px;
        }

        .process-item.active {
            background: #4fc3f7;
            color: #121212;
            border-color: #4fc3f7;
            font-weight: 600;
        }

        .process-item:hover {
            border-color: #4fc3f7;
        }

        /* 输入框 */
        .input-group {
            margin-bottom: 16px;
        }

        .input-group label {
            display: block;
            margin-bottom: 6px;
            color: #4fc3f7;
            font-size: 14px;
        }

        .input-group input,
        .input-group textarea {
            width: 100%;
            padding: 12px;
            background: #2d2d2d;
            border: 1px solid #3d3d3d;
            border-radius: 8px;
            color: #fff;
            font-size: 14px;
            outline: none;
            transition: border 0.3s;
        }

        .input-group input:focus,
        .input-group textarea:focus {
            border-color: #4fc3f7;
        }

        .input-group textarea {
            min-height: 80px;
            resize: none;
        }

        /* 按钮 */
        .btn {
            width: 100%;
            padding: 14px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 10px;
        }

        .btn-primary {
            background: #4fc3f7;
            color: #121212;
        }

        .btn-primary:hover {
            background: #29b6f6;
        }

        .btn-secondary {
            background: #7e57c2;
            color: #fff;
        }

        .btn-secondary:hover {
            background: #673ab7;
        }

        .btn:disabled {
            background: #3d3d3d;
            cursor: not-allowed;
            opacity: 0.6;
        }

        /* 统计面板 */
        .stats-panel {
            display: flex;
            flex-direction: column;
            gap: 12px;
            text-align: center;
        }

        .stat-item {
            padding: 12px;
            background: #2d2d2d;
            border-radius: 8px;
        }

        .stat-item.success {
            border-left: 4px solid #4caf50;
        }

        .stat-item.fail {
            border-left: 4px solid #f44336;
        }

        .stat-item.total {
            border-left: 4px solid #fff;
        }

        .stat-item.progress {
            border-left: 4px solid #ff9800;
        }

        .stat-value {
            font-size: 28px;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .stat-label {
            font-size: 14px;
            opacity: 0.8;
        }

        /* 日志 */
        .log-container {
            margin-top: 16px;
        }

        .log-header {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
        }

        .log-btn {
            padding: 6px 12px;
            background: #4fc3f7;
            color: #121212;
            border: none;
            border-radius: 6px;
            font-size: 12px;
            cursor: pointer;
        }

        .log-box {
            background: #1e1e1e;
            border: 1px solid #3d3d3d;
            border-radius: 8px;
            padding: 12px;
            height: 200px;
            overflow-y: auto;
            font-size: 13px;
            line-height: 1.6;
        }

        .log-item {
            margin-bottom: 8px;
            display: flex;
            gap: 8px;
        }

        .log-time {
            color: #ff9800;
            flex-shrink: 0;
        }

        .log-type {
            color: #4fc3f7;
            flex-shrink: 0;
        }

        .log-content {
            flex: 1;
        }

        /* 解析结果 */
        .result-box {
            background: #2d2d2d;
            border-radius: 8px;
            padding: 12px;
            margin-top: 12px;
            font-size: 13px;
            line-height: 1.6;
        }

        .result-box p {
            margin-bottom: 6px;
        }

        .result-box .label {
            color: #4fc3f7;
            font-weight: 500;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 头部 -->
        <div class="header">
            <h1>快手速刷工具</h1>
            <p>网站版 - 高效批量评论系统</p>
        </div>

        <!-- 进程选择 -->
        <div class="module">
            <div class="module-title">
                <span>⚙️</span>选择进程
            </div>
            <div class="process-list">
                <div class="process-item active" data-process="1">进程 1</div>
                <div class="process-item" data-process="2">进程 2</div>
                <div class="process-item" data-process="3">进程 3</div>
                <div class="process-item" data-process="4">进程 4</div>
            </div>
        </div>

        <!-- 输入区域 -->
        <div class="module">
            <div class="module-title">
                <span>🔗</span>快手作品链接
            </div>
            <div class="input-group">
                <input type="text" id="videoUrl" placeholder="请输入快手作品链接">
            </div>

            <div class="module-title">
                <span>✍️</span>评论内容
            </div>
            <div class="input-group">
                <textarea id="commentContent" placeholder="请输入评论内容，支持多行，随机发送"></textarea>
            </div>

            <div class="module-title">
                <span>🔄</span>重试次数
            </div>
            <div class="input-group">
                <input type="number" id="retryCount" value="3" placeholder="失败后重试次数">
            </div>

            <button class="btn btn-primary" id="parseBtn">解析链接</button>
            <button class="btn btn-secondary" id="startBtn" disabled>开始任务</button>
        </div>

        <!-- 解析结果 -->
        <div class="module" id="resultModule" style="display: none;">
            <div class="module-title">
                <span>🔍</span>解析结果
            </div>
            <div class="result-box" id="resultBox">
                <p><span class="label">用户ID:</span> <span id="userId">-</span></p>
                <p><span class="label">作品ID:</span> <span id="photoId">-</span></p>
                <p><span class="label">原始链接:</span> <span id="originalUrl">-</span></p>
            </div>
        </div>

        <!-- 统计面板 -->
        <div class="module">
            <div class="stats-panel">
                <div class="stat-item success">
                    <div class="stat-value" id="successCount">0</div>
                    <div class="stat-label">成功</div>
                </div>
                <div class="stat-item fail">
                    <div class="stat-value" id="failCount">0</div>
                    <div class="stat-label">失败</div>
                </div>
                <div class="stat-item total">
                    <div class="stat-value" id="totalCount">0</div>
                    <div class="stat-label">总数</div>
                </div>
                <div class="stat-item progress">
                    <div class="stat-value" id="progressPercent">0%</div>
                    <div class="stat-label">进度</div>
                </div>
            </div>
        </div>

        <!-- 日志区域 -->
        <div class="module">
            <div class="module-title">
                <span>📝</span>实时日志
            </div>
            <div class="log-container">
                <div class="log-header">
                    <button class="log-btn" id="clearLog">清空日志</button>
                    <button class="log-btn" id="pauseScroll">暂停滚动</button>
                </div>
                <div class="log-box" id="logBox">
                    <div class="log-item">
                        <span class="log-time">系统</span>
                        <span class="log-type">系统</span>
                        <span class="log-content">系统初始化完成，请输入作品链接并点击解析链接</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // DOM元素
        const processItems = document.querySelectorAll('.process-item');
        const videoUrl = document.getElementById('videoUrl');
        const commentContent = document.getElementById('commentContent');
        const retryCount = document.getElementById('retryCount');
        const parseBtn = document.getElementById('parseBtn');
        const startBtn = document.getElementById('startBtn');
        const resultModule = document.getElementById('resultModule');
        const resultBox = document.getElementById('resultBox');
        const userId = document.getElementById('userId');
        const photoId = document.getElementById('photoId');
        const originalUrl = document.getElementById('originalUrl');
        const successCount = document.getElementById('successCount');
        const failCount = document.getElementById('failCount');
        const totalCount = document.getElementById('totalCount');
        const progressPercent = document.getElementById('progressPercent');
        const logBox = document.getElementById('logBox');
        const clearLog = document.getElementById('clearLog');
        const pauseScroll = document.getElementById('pauseScroll');

        // 状态
        let currentProcess = 1;
        let isScrollPaused = false;
        let isParsing = false;
        let isRunning = false;
        let parseResult = null;
        let commentList = [];
        let taskCount = 0;
        let success = 0;
        let fail = 0;

        // 进程选择
        processItems.forEach(item => {
            item.addEventListener('click', () => {
                processItems.forEach(i => i.classList.remove('active'));
                item.classList.add('active');
                currentProcess = parseInt(item.dataset.process);
                addLog(`已选择进程 ${currentProcess}`, '系统');
            });
        });

        // 添加日志
        function addLog(content, type = '系统') {
            const time = new Date().toLocaleTimeString();
            const logItem = document.createElement('div');
            logItem.className = 'log-item';
            logItem.innerHTML = `
                <span class="log-time">${time}</span>
                <span class="log-type">${type}</span>
                <span class="log-content">${content}</span>
            `;
            logBox.appendChild(logItem);
            if (!isScrollPaused) {
                logBox.scrollTop = logBox.scrollHeight;
            }
        }

        // 清空日志
        clearLog.addEventListener('click', () => {
            logBox.innerHTML = '';
            addLog('日志已清空', '系统');
        });

        // 暂停滚动
        pauseScroll.addEventListener('click', () => {
            isScrollPaused = !isScrollPaused;
            pauseScroll.textContent = isScrollPaused ? '恢复滚动' : '暂停滚动';
        });

        // 解析链接
        parseBtn.addEventListener('click', async () => {
            const url = videoUrl.value.trim();
            if (!url) {
                alert('请输入快手作品链接');
                return;
            }

            isParsing = true;
            parseBtn.disabled = true;
            parseBtn.textContent = '解析中...';
            addLog('开始解析作品链接...', '系统');

            try {
                // 模拟解析
                await new Promise(resolve => setTimeout(resolve, 1500));
                
                // 模拟解析结果
                parseResult = {
                    userId: `3xz2tw6n4bxe96qg`,
                    photoId: `3x4v45g3db5yrbk`,
                    originalUrl: url
                };

                // 更新UI
                userId.textContent = parseResult.userId;
                photoId.textContent = parseResult.photoId;
                originalUrl.textContent = parseResult.originalUrl;
                resultModule.style.display = 'block';
                startBtn.disabled = false;
                addLog('作品链接解析成功', '系统');
            } catch (error) {
                addLog(`解析失败: ${error.message}`, '系统');
            } finally {
                isParsing = false;
                parseBtn.disabled = false;
                parseBtn.textContent = '解析链接';
            }
        });

        // 开始任务
        startBtn.addEventListener('click', async () => {
            if (!parseResult) {
                alert('请先解析作品链接');
                return;
            }

            const comments = commentContent.value.trim().split('\n').filter(c => c.trim());
            if (comments.length === 0) {
                alert('请输入至少一条评论内容');
                return;
            }

            commentList = comments;
            taskCount = 8; // 模拟任务数量
            success = 0;
            fail = 0;

            isRunning = true;
            startBtn.disabled = true;
            startBtn.textContent = '任务执行中...';
            addLog(`任务已启动，开始处理 ${taskCount} 条评论`, '系统');

            // 初始化统计
            successCount.textContent = '0';
            failCount.textContent = '0';
            totalCount.textContent = taskCount;
            progressPercent.textContent = '0%';

            // 模拟任务执行
            for (let i = 0; i < taskCount; i++) {
                if (!isRunning) break;

                try {
                    // 模拟接口请求
                    await new Promise(resolve => setTimeout(resolve, 1000));
                    
                    // 模拟随机成功/失败
                    const isSuccess = Math.random() > 0.2;
                    if (isSuccess) {
                        success++;
                        successCount.textContent = success;
                        addLog(`评论发送成功: ${commentList[Math.floor(Math.random() * commentList.length)]}`, '成功');
                    } else {
                        fail++;
                        failCount.textContent = fail;
                        addLog('评论发送失败，正在重试...', '失败');
                    }

                    // 更新进度
                    const progress = Math.round(((i + 1) / taskCount) * 100);
                    progressPercent.textContent = `${progress}%`;
                } catch (error) {
                    fail++;
                    failCount.textContent = fail;
                    addLog(`任务失败: ${error.message}`, '失败');
                }
            }

            // 任务完成
            isRunning = false;
            startBtn.disabled = false;
            startBtn.textContent = '开始任务';
            addLog(`任务完成: 成功 ${success} 条，失败 ${fail} 条`, '系统');
        });
    </script>
</body>
</html>
