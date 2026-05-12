<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.5, user-scalable=yes">
    <title>菜园奇遇记 · 植物病虫害探究</title>
    <style>
        :root {
            --green-50: #f0fdf4;
            --green-100: #dcfce7;
            --green-200: #bbf7d0;
            --green-400: #4ade80;
            --green-500: #22c55e;
            --green-600: #16a34a;
            --green-700: #15803d;
            --green-800: #166534;
            --amber-50: #fffbeb;
            --amber-100: #fef3c7;
            --amber-400: #fbbf24;
            --amber-600: #d97706;
            --red-50: #fef2f2;
            --red-100: #fee2e2;
            --red-500: #ef4444;
            --gray-50: #f9fafb;
            --gray-100: #f3f4f6;
            --gray-200: #e5e7eb;
            --gray-300: #d1d5db;
            --gray-400: #9ca3af;
            --gray-500: #6b7280;
            --gray-600: #4b5563;
            --gray-700: #374151;
            --gray-800: #1f2937;
            --gray-900: #111827;
            --white: #ffffff;
            --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
            --shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.05);
            --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.08);
            --shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.1);
            --radius-sm: 8px;
            --radius: 12px;
            --radius-lg: 16px;
            --radius-xl: 20px;
            --radius-2xl: 24px;
            --transition: 0.25s cubic-bezier(0.4, 0, 0.2, 1);
            --safe-bottom: env(safe-area-inset-bottom, 16px);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'PingFang SC', 'Microsoft YaHei', 'Hiragino Sans GB', sans-serif;
            background: linear-gradient(160deg, #f0fdf4 0%, #dcfce7 30%, #f8fafc 60%, #fefce8 100%);
            background-attachment: fixed;
            min-height: 100vh;
            color: var(--gray-800);
            line-height: 1.6;
            -webkit-tap-highlight-color: transparent;
            -webkit-font-smoothing: antialiased;
            padding: 12px 12px calc(80px + var(--safe-bottom));
        }

        .app-container {
            max-width: 700px;
            margin: 0 auto;
        }

        /* 顶部导航栏 */
        .top-bar {
            background: var(--white);
            border-radius: 30px;
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: var(--shadow-md);
            position: sticky;
            top: 8px;
            z-index: 30;
            margin-bottom: 14px;
            border: 1px solid var(--gray-100);
        }
        .top-bar .title {
            font-weight: 700;
            font-size: 17px;
            color: var(--green-700);
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .coin-badge {
            background: #fef3c7;
            padding: 6px 14px;
            border-radius: 20px;
            font-weight: 700;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 4px;
            color: #92400e;
            border: 1px solid #fde68a;
        }

        /* 页面容器 */
        .page {
            display: none;
            animation: fadeSlide 0.4s ease;
        }
        .page.active {
            display: block;
        }
        @keyframes fadeSlide {
            from {
                opacity: 0;
                transform: translateY(16px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* 卡片 */
        .card {
            background: var(--white);
            border-radius: var(--radius-2xl);
            padding: 20px 18px;
            box-shadow: var(--shadow-lg);
            margin-bottom: 16px;
            border: 1px solid rgba(0, 0, 0, 0.03);
            position: relative;
            overflow: hidden;
        }
        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, #22c55e, #4ade80, #86efac);
            border-radius: 0 0 6px 6px;
            opacity: 0.5;
        }
        .card h2 {
            font-size: 20px;
            font-weight: 700;
            color: var(--green-800);
            margin-bottom: 6px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .card h3 {
            font-size: 17px;
            font-weight: 700;
            color: var(--gray-800);
            margin: 10px 0 6px;
        }
        .card p {
            font-size: 14px;
            color: var(--gray-600);
            margin: 4px 0;
        }

        /* 按钮 */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
            padding: 11px 22px;
            border-radius: 30px;
            font-weight: 600;
            border: none;
            cursor: pointer;
            font-size: 14px;
            transition: all var(--transition);
            letter-spacing: 0.2px;
            white-space: nowrap;
        }
        .btn:active {
            transform: scale(0.96);
        }
        .btn-primary {
            background: var(--green-600);
            color: white;
            box-shadow: 0 4px 14px rgba(22, 163, 74, 0.3);
        }
        .btn-primary:hover {
            background: var(--green-700);
            box-shadow: 0 6px 20px rgba(22, 163, 74, 0.4);
        }
        .btn-outline {
            background: var(--white);
            color: var(--green-700);
            border: 2px solid var(--green-400);
        }
        .btn-outline:hover {
            background: var(--green-50);
            border-color: var(--green-500);
        }
        .btn-sm {
            padding: 6px 14px;
            font-size: 12px;
            border-radius: 20px;
        }
        .btn-warn {
            background: #fef3c7;
            color: #92400e;
            border: 1px solid #fde68a;
        }
        .btn-full {
            width: 100%;
            margin-top: 10px;
        }

        /* 网格 */
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }
        @media (max-width: 480px) {
            .grid-2 {
                grid-template-columns: 1fr;
            }
        }

        /* 上传区域 */
        .upload-zone {
            border: 2.5px dashed var(--gray-300);
            border-radius: var(--radius-xl);
            padding: 28px 18px;
            text-align: center;
            cursor: pointer;
            transition: all var(--transition);
            background: var(--gray-50);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            user-select: none;
        }
        .upload-zone:hover {
            border-color: var(--green-400);
            background: var(--green-50);
            transform: translateY(-1px);
        }
        .upload-zone .icon {
            font-size: 46px;
            transition: transform var(--transition);
        }
        .upload-zone:hover .icon {
            transform: scale(1.1);
        }

        /* 进度条 */
        .prob-bar {
            height: 8px;
            border-radius: 4px;
            background: var(--gray-100);
            margin: 4px 0;
            overflow: hidden;
        }
        .prob-fill {
            height: 100%;
            border-radius: 4px;
            transition: width 0.6s ease;
        }

        /* 提示卡片 */
        .hint-card {
            background: #fffbeb;
            border: 1px solid #fde68a;
            border-radius: var(--radius-lg);
            padding: 12px 14px;
            margin: 8px 0;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 10px;
        }
        .hint-card span {
            font-size: 13px;
            font-weight: 500;
            color: #92400e;
        }

        /* 证据方法 */
        .evidence-card {
            background: var(--gray-50);
            border-radius: var(--radius-lg);
            padding: 14px;
            cursor: pointer;
            border: 1px solid var(--gray-100);
            text-align: center;
            transition: all var(--transition);
        }
        .evidence-card:hover {
            background: var(--green-50);
            border-color: var(--green-300);
            transform: translateY(-2px);
            box-shadow: var(--shadow-md);
        }
        .evidence-card .icon {
            font-size: 36px;
            margin-bottom: 6px;
        }
        .evidence-card .title {
            font-weight: 700;
            font-size: 14px;
            margin-bottom: 2px;
        }
        .evidence-card .desc {
            font-size: 11px;
            color: var(--gray-500);
        }

        /* 模态框 */
        .modal-overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.5);
            z-index: 100;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(3px);
            -webkit-backdrop-filter: blur(3px);
        }
        .modal-overlay.show {
            display: flex;
        }
        .modal-box {
            background: var(--white);
            border-radius: var(--radius-2xl);
            padding: 20px 18px;
            width: 90%;
            max-width: 440px;
            max-height: 78vh;
            overflow-y: auto;
            box-shadow: var(--shadow-xl);
            animation: popIn 0.3s ease;
        }
        @keyframes popIn {
            from {
                opacity: 0;
                transform: scale(0.85) translateY(20px);
            }
            to {
                opacity: 1;
                transform: scale(1) translateY(0);
            }
        }

        /* AI聊天窗口 */
        .chat-window {
            background: var(--gray-50);
            border-radius: var(--radius-lg);
            border: 1px solid var(--gray-200);
            padding: 10px;
            max-height: 260px;
            overflow-y: auto;
            margin: 10px 0;
            display: flex;
            flex-direction: column;
            gap: 6px;
        }
        .chat-bubble {
            max-width: 85%;
            padding: 8px 14px;
            border-radius: 18px;
            font-size: 13px;
            line-height: 1.5;
            word-break: break-word;
        }
        .chat-bot {
            background: var(--green-50);
            align-self: flex-start;
            border-bottom-left-radius: 4px;
        }
        .chat-user {
            background: var(--green-600);
            color: white;
            align-self: flex-end;
            border-bottom-right-radius: 4px;
        }

        /* 标签 */
        .tag {
            display: inline-block;
            padding: 3px 10px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 600;
            letter-spacing: 0.3px;
        }
        .tag-green {
            background: #dcfce7;
            color: #166534;
        }
        .tag-amber {
            background: #fef3c7;
            color: #92400e;
        }
        .tag-red {
            background: #fee2e2;
            color: #b91c1c;
        }

        /* 评价量表 */
        .rubric-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 13px;
            margin: 12px 0;
        }
        .rubric-table th,
        .rubric-table td {
            padding: 8px 6px;
            border: 1px solid var(--gray-200);
            text-align: center;
        }
        .rubric-table th {
            background: var(--green-50);
            font-weight: 700;
            color: var(--green-800);
            font-size: 12px;
        }
        .rubric-table input[type="checkbox"] {
            width: 18px;
            height: 18px;
            cursor: pointer;
            accent-color: var(--green-600);
        }

        /* Toast */
        .toast {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--gray-900);
            color: white;
            padding: 12px 24px;
            border-radius: 25px;
            font-size: 14px;
            font-weight: 500;
            z-index: 200;
            opacity: 0;
            transition: all 0.35s ease;
            pointer-events: none;
            box-shadow: var(--shadow-xl);
        }
        .toast.show {
            opacity: 1;
            top: 30px;
        }

        /* 底部导航 */
        .bottom-nav {
            position: fixed;
            bottom: 10px;
            left: 10px;
            right: 10px;
            background: rgba(255, 255, 255, 0.92);
            border-radius: 28px;
            padding: 6px 8px;
            display: flex;
            justify-content: space-around;
            align-items: center;
            box-shadow: 0 -2px 16px rgba(0, 0, 0, 0.06);
            z-index: 40;
            max-width: 700px;
            margin: 0 auto;
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(0, 0, 0, 0.04);
        }
        .nav-btn {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 2px;
            padding: 6px 2px;
            border-radius: 16px;
            cursor: pointer;
            transition: 0.2s;
            font-size: 10px;
            color: var(--gray-500);
            border: none;
            background: transparent;
            font-weight: 500;
            letter-spacing: 0.3px;
        }
        .nav-btn.active {
            color: var(--green-700);
            font-weight: 700;
        }
        .nav-btn .nav-icon {
            font-size: 20px;
        }

        /* 语音按钮 */
        .voice-btn {
            background: #fef3c7;
            border: 2px solid #fde68a;
            border-radius: 30px;
            padding: 10px 20px;
            display: flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 14px;
            transition: all 0.2s;
        }
        .voice-btn:active {
            background: #fde68a;
        }
        textarea,
        input[type="text"] {
            border: 1.5px solid var(--gray-300);
            border-radius: 14px;
            padding: 10px 14px;
            font-size: 14px;
            width: 100%;
            font-family: inherit;
            transition: border-color 0.2s;
        }
        textarea:focus,
        input[type="text"]:focus {
            border-color: var(--green-400);
            outline: none;
        }

        /* 等级徽章动画 */
        @keyframes pulse {
            0%,
            100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.08);
            }
        }
        .level-badge {
            display: inline-block;
            padding: 8px 20px;
            border-radius: 24px;
            font-weight: 700;
            font-size: 16px;
            animation: pulse 1.5s ease infinite;
        }
    </style>
</head>
<body>

    <div class="app-container">
        <!-- 顶部栏 -->
        <div class="top-bar">
            <span class="title">🌱 菜园奇遇记</span>
            <span class="coin-badge" id="coinDisplay">🕵️ 侦探币 10</span>
        </div>

        <!-- 页面1：提出问题（封面） -->
        <div class="page active" id="page1">
            <div class="card" style="text-align:center; background:linear-gradient(135deg,#f0fdf4 0%,#fffbeb 50%,#fefce8 100%); padding:32px 20px;">
                <div style="font-size:72px; animation: pulse 2s ease infinite;">🥬🔍</div>
                <h1 style="font-size:30px;color:var(--green-800);margin:8px 0;letter-spacing:-0.5px;">菜园奇遇记</h1>
                <p style="font-size:16px;color:#4b5563;font-weight:500;margin-bottom:4px;">小侦探的"白菜危机"探究行动</p>
                <p style="font-size:13px;color:var(--gray-500);max-width:320px;margin:8px auto;line-height:1.7;">
                    学校菜园里，许多白菜叶片卷曲发黄、布满小虫……<br>到底是谁在捣乱？<br>让我们一起像科学家那样寻找真相！
                </p>
                <button class="btn btn-primary" style="margin-top:14px;font-size:16px;padding:13px 30px;" onclick="navigateTo('page2')">🚀 开始探究</button>
            </div>
        </div>

        <!-- 页面2：作出假设（拍照识别） -->
        <div class="page" id="page2">
            <div class="card">
                <h2>📸 拍照识别 · 作出假设</h2>
                <p style="font-size:13px;color:var(--gray-500);">上传白菜叶片照片，AI将给出初步判断</p>
                <div class="upload-zone" id="uploadZone2" style="margin-top:10px;">
                    <span class="icon">📷</span>
                    <span style="font-weight:600;">点击上传叶片照片</span>
                    <span style="font-size:11px;color:var(--gray-400);">支持 JPG / PNG</span>
                </div>
                <input type="file" id="fileInput2" accept="image/*" style="display:none;">
                <div id="previewArea2" style="display:none; margin-top:12px;">
                    <img id="previewImg2" style="width:100%; max-height:200px; object-fit:contain; border-radius:16px; background:#1a1a1a;" alt="">
                    <button class="btn btn-primary btn-full" onclick="analyzeImage()">🔬 开始分析</button>
                </div>
                <div id="resultArea2" style="margin-top:14px;"></div>
            </div>
        </div>

        <!-- 页面3：设计方案 -->
        <div class="page" id="page3">
            <div class="card">
                <h2>📋 设计方案</h2>
                <p style="font-size:13px;color:var(--gray-500);">我们还需要调查哪些证据，证明蚜虫是让白菜生病的真凶？</p>
                <div style="margin:10px 0;">
                    <button class="voice-btn" id="voiceBtn">🎤 语音输入方案</button>
                    <span style="font-size:11px;color:var(--gray-400);margin-left:8px;">点击后说话</span>
                </div>
                <textarea id="planText" placeholder="写下或说出你的调查方案，例如：观察蚜虫的形态特征、调查白菜病害症状……" rows="4"></textarea>

                <p style="font-weight:700;margin-top:14px;color:var(--amber-600);">💡 调查提示卡片 <span style="font-size:11px;font-weight:400;color:var(--gray-400);">(点击消耗侦探币)</span></p>
                <div class="hint-card" id="hintCard1">
                    <span>🔍 提示1：蚜虫的基本信息探秘</span>
                    <button class="btn btn-sm btn-warn" onclick="buyHint(1)">-1币 查看</button>
                </div>
                <div class="hint-card" id="hintCard2">
                    <span>🌡️ 提示2：蚜虫的"宜居环境"大揭秘</span>
                    <button class="btn btn-sm btn-warn" onclick="buyHint(2)">-1币 查看</button>
                </div>
                <div class="hint-card" id="hintCard3">
                    <span>🥬 提示3：蚜虫与白菜的"关联性"</span>
                    <button class="btn btn-sm btn-warn" onclick="buyHint(3)">-1币 查看</button>
                </div>
                <div id="hintContent" style="background:#f3f4f6; border-radius:14px; padding:14px; margin-top:10px; display:none;"></div>
            </div>
        </div>

        <!-- 页面4：搜集证据 -->
        <div class="page" id="page4">
            <div class="card">
                <h2>🔎 搜集证据</h2>
                <p style="font-size:13px;color:var(--gray-500);">点击对应图标，选择调查方法</p>
                <div class="grid-2" style="margin-top:12px;">
                    <div class="evidence-card" onclick="openEvidence('book')">
                        <div class="icon">📖</div>
                        <div class="title">权威书籍</div>
                        <div class="desc">查看蚜虫身份信息</div>
                    </div>
                    <div class="evidence-card" onclick="openEvidence('image')">
                        <div class="icon">🖼️</div>
                        <div class="title">图像与AR</div>
                        <div class="desc">照片 & 三维模型</div>
                    </div>
                    <div class="evidence-card" onclick="openEvidence('ai')">
                        <div class="icon">🤖</div>
                        <div class="title">AI专家沟通</div>
                        <div class="desc">厦门本土专家</div>
                    </div>
                    <div class="evidence-card" onclick="openEvidence('observe')">
                        <div class="icon">🔬</div>
                        <div class="title">实物观察</div>
                        <div class="desc">放大镜观察蚜虫</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 页面5：汇报交流 -->
        <div class="page" id="page5">
            <div class="card">
                <h2>🏆 汇报交流 · 侦探积分</h2>
                <p style="font-size:13px;color:var(--gray-500);">像科学家那样探究！请根据你们小组的实际表现，在以下评价标准中打勾：</p>

                <div style="margin:10px 0;">
                    <label style="font-weight:600;">选择小组：</label>
                    <select id="groupSelect" style="padding:8px 12px;border-radius:14px;border:1px solid var(--gray-300);font-size:14px;">
                        <option>第1小组</option><option>第2小组</option><option>第3小组</option><option>第4小组</option>
                        <option>第5小组</option><option>第6小组</option>
                    </select>
                </div>

                <!-- 评价量表 -->
                <table class="rubric-table" id="rubricTable">
                    <thead>
                        <tr>
                            <th>评价维度</th>
                            <th>评价指标</th>
                            <th>达成✓</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td rowspan="2"><strong>🔍 提出问题<br>与作出假设</strong></td>
                            <td>能基于观察提出可探究的科学问题</td>
                            <td><input type="checkbox" class="rubric-check" data-score="2"></td>
                        </tr>
                        <tr>
                            <td>能对问题作出有依据的假设（如猜测是蚜虫危害）</td>
                            <td><input type="checkbox" class="rubric-check" data-score="2"></td>
                        </tr>
                        <tr>
                            <td rowspan="2"><strong>📋 制定计划<br>与搜集证据</strong></td>
                            <td>能制定简单的调查方案，明确需要搜集哪些证据</td>
                            <td><input type="checkbox" class="rubric-check" data-score="2"></td>
                        </tr>
                        <tr>
                            <td>能使用多种方法（观察、查阅资料、AI咨询等）搜集证据</td>
                            <td><input type="checkbox" class="rubric-check" data-score="2"></td>
                        </tr>
                        <tr>
                            <td rowspan="2"><strong>📊 处理信息<br>与分析数据</strong></td>
                            <td>能记录和整理搜集到的信息（文字、图画、表格等）</td>
                            <td><input type="checkbox" class="rubric-check" data-score="2"></td>
                        </tr>
                        <tr>
                            <td>能依据证据分析问题，辨别AI给出的不同可能性</td>
                            <td><input type="checkbox" class="rubric-check" data-score="2"></td>
                        </tr>
                        <tr>
                            <td rowspan="2"><strong>💬 得出结论<br>与表达交流</strong></td>
                            <td>能基于证据得出结论（如确认蚜虫是危害白菜的真凶）</td>
                            <td><input type="checkbox" class="rubric-check" data-score="2"></td>
                        </tr>
                        <tr>
                            <td>能清晰地向他人表达探究过程和结果</td>
                            <td><input type="checkbox" class="rubric-check" data-score="2"></td>
                        </tr>
                        <tr>
                            <td rowspan="2"><strong>🌟 反思评价<br>与责任态度</strong></td>
                            <td>能反思探究过程中的不足，提出改进建议</td>
                            <td><input type="checkbox" class="rubric-check" data-score="1"></td>
                        </tr>
                        <tr>
                            <td>表现出对植物保护的责任感，愿意采取行动</td>
                            <td><input type="checkbox" class="rubric-check" data-score="1"></td>
                        </tr>
                    </tbody>
                </table>

                <button class="btn btn-primary btn-full" onclick="calculateLevel()">📊 计算侦探等级</button>
                <div id="levelResult" style="text-align:center; margin-top:14px; font-size:18px; font-weight:700;"></div>
                <p style="text-align:center;font-size:13px;color:var(--gray-500);margin-top:6px;">
                    剩余侦探币：<strong id="finalCoins">10</strong> 🪙
                </p>
            </div>
        </div>
    </div>

    <!-- 底部导航 -->
    <div class="bottom-nav">
        <button class="nav-btn active" data-page="page1"><span class="nav-icon">🏠</span>封面</button>
        <button class="nav-btn" data-page="page2"><span class="nav-icon">📸</span>假设</button>
        <button class="nav-btn" data-page="page3"><span class="nav-icon">📋</span>方案</button>
        <button class="nav-btn" data-page="page4"><span class="nav-icon">🔍</span>证据</button>
        <button class="nav-btn" data-page="page5"><span class="nav-icon">🏆</span>交流</button>
    </div>

    <!-- 模态层 -->
    <div class="modal-overlay" id="modalOverlay">
        <div class="modal-box" id="modalContent"></div>
    </div>

    <!-- Toast -->
    <div class="toast" id="toast"></div>

    <script>
        (function() {
            // ============ 全局状态 ============
            let detectiveCoins = 10;
            let currentPage = 'page1';

            const coinDisplay = document.getElementById('coinDisplay');
            const finalCoinsEl = document.getElementById('finalCoins');
            const modalOverlay = document.getElementById('modalOverlay');
            const modalContent = document.getElementById('modalContent');
            const toast = document.getElementById('toast');
            const planText = document.getElementById('planText');
            const hintContent = document.getElementById('hintContent');
            const previewArea2 = document.getElementById('previewArea2');
            const previewImg2 = document.getElementById('previewImg2');
            const resultArea2 = document.getElementById('resultArea2');
            const uploadZone2 = document.getElementById('uploadZone2');
            const fileInput2 = document.getElementById('fileInput2');

            // ============ 工具函数 ============
            function updateCoinDisplay() {
                coinDisplay.textContent = '🕵️ 侦探币 ' + detectiveCoins;
                if (finalCoinsEl) finalCoinsEl.textContent = detectiveCoins;
            }

            function showToast(msg, duration = 2000) {
                toast.textContent = msg;
                toast.classList.add('show');
                clearTimeout(toast._timeout);
                toast._timeout = setTimeout(() => toast.classList.remove('show'), duration);
            }

            function spendCoin(amount = 1) {
                if (detectiveCoins >= amount) {
                    detectiveCoins -= amount;
                    updateCoinDisplay();
                    return true;
                } else {
                    showToast('侦探币不足！继续探究收集更多线索吧 🔍');
                    return false;
                }
            }

            function addCoin(amount = 1) {
                detectiveCoins += amount;
                updateCoinDisplay();
            }

            // ============ 页面导航 ============
            function navigateTo(pageId) {
                document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
                const target = document.getElementById(pageId);
                if (target) target.classList.add('active');
                currentPage = pageId;
                document.querySelectorAll('.nav-btn').forEach(btn => {
                    btn.classList.remove('active');
                    if (btn.dataset.page === pageId) btn.classList.add('active');
                });
                window.scrollTo({ top: 0, behavior: 'smooth' });
                if (pageId === 'page5') updateCoinDisplay();
            }

            // 底部导航事件
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    navigateTo(this.dataset.page);
                });
            });

            // ============ 模态框 ============
            function openModal(html) {
                modalContent.innerHTML = html +
                    '<button class="btn btn-outline" style="width:100%;margin-top:12px;" onclick="closeModal()">关闭 ✕</button>';
                modalOverlay.classList.add('show');
            }

            window.closeModal = function() {
                modalOverlay.classList.remove('show');
            };
            modalOverlay.addEventListener('click', function(e) {
                if (e.target === modalOverlay) closeModal();
            });

            // ============ 页面2：拍照识别 ============
            uploadZone2.addEventListener('click', () => fileInput2.click());
            fileInput2.addEventListener('change', function(e) {
                const file = e.target.files[0];
                if (!file) return;
                const reader = new FileReader();
                reader.onload = function(ev) {
                    previewImg2.src = ev.target.result;
                    previewArea2.style.display = 'block';
                    resultArea2.innerHTML = '';
                };
                reader.readAsDataURL(file);
            });

            window.analyzeImage = function() {
                if (!previewImg2.src || previewImg2.src === window.location.href) {
                    showToast('请先上传叶片照片 📸');
                    return;
                }
                resultArea2.innerHTML = `
                <div style="background:#f9fafb;border-radius:16px;padding:16px;margin-top:10px;border:1px solid var(--gray-100);">
                  <p style="font-weight:700;font-size:15px;">📊 AI 初步判断</p>
                  <p style="font-size:12px;color:var(--gray-500);margin-bottom:10px;">基于叶片颜色特征分析，匹配结果如下：</p>
                  <div style="margin:8px 0;">
                    <div style="display:flex;justify-content:space-between;font-size:14px;font-weight:600;">
                      <span>🐛 蚜虫侵害</span><span style="color:var(--green-700);">78%</span>
                    </div>
                    <div class="prob-bar"><div class="prob-fill" style="width:78%;background:var(--green-500);"></div></div>
                  </div>
                  <div style="margin:8px 0;">
                    <div style="display:flex;justify-content:space-between;font-size:13px;">
                      <span>🍂 白粉病</span><span>12%</span>
                    </div>
                    <div class="prob-bar"><div class="prob-fill" style="width:12%;background:#fbbf24;"></div></div>
                  </div>
                  <div style="margin:8px 0;">
                    <div style="display:flex;justify-content:space-between;font-size:13px;">
                      <span>🟤 叶斑病</span><span>10%</span>
                    </div>
                    <div class="prob-bar"><div class="prob-fill" style="width:10%;background:#f87171;"></div></div>
                  </div>
                  <p style="font-size:12px;color:#dc2626;margin-top:8px;font-weight:600;">⚠️ AI提示不代表准确答案，需要同学们进一步探究。</p>
                  <p style="font-size:13px;margin-top:6px;"><strong>🔬 部分防治方式参考：</strong>悬挂黄板诱杀有翅蚜、释放瓢虫等天敌、喷洒肥皂水或苦参碱。</p>
                  <button class="btn btn-primary btn-full" onclick="navigateTo('page3')">📋 去设计方案 →</button>
                </div>`;
                addCoin(1);
            };

            // ============ 页面3：设计方案 ============
            window.buyHint = function(num) {
                if (!spendCoin(1)) return;
                const hints = {
                    1: '🔍 蚜虫基本信息探秘：<br><br>调查内容可以从<strong>形态特征</strong>入手——蚜虫体长1-2毫米，身体柔软，颜色多样（绿、黄、黑、红等），腹部有一对管状结构的"腹管"，触角较长。有翅蚜和无翅蚜形态不同。建议用放大镜仔细观察虫体颜色、大小、有无翅膀等特征。',
                    2: '🌡️ 蚜虫"宜居环境"大揭秘：<br><br>如果你是蚜虫，你会选择什么样的环境安家？蚜虫喜欢<strong>温暖（16-25℃）、干燥少雨</strong>的天气。厦门春季气温回升后，连续晴好天气最利于蚜虫繁殖。当气温超过30℃或连续大雨时，蚜虫数量会明显下降。想一想：最近厦门的天气是不是很适合蚜虫生长？',
                    3: '🥬 蚜虫与白菜的"关联性"：<br><br>蚜虫是不是只"偏爱"白菜呢？事实上，蚜虫（特别是菜蚜类）主要危害<strong>十字花科蔬菜</strong>，包括白菜、萝卜、油菜、甘蓝等。当白菜遭遇蚜虫侵袭，会留下独特的痕迹：<strong>叶片卷曲发黄、出现黏腻蜜露、常伴有蚂蚁活动、植株矮小生长缓慢</strong>，严重时还可传播病毒病。'
                };
                hintContent.style.display = 'block';
                hintContent.innerHTML = hints[num];
                if (planText.value.trim() === '') {
                    planText.value = hints[num].replace(/<[^>]*>/g, '').replace(/&[^;]+;/g, '').substring(0, 200) +
                        '...';
                }
                // 高亮已购买的提示卡片
                const cardId = 'hintCard' + num;
                const card = document.getElementById(cardId);
                if (card) {
                    card.style.background = '#dcfce7';
                    card.querySelector('button').textContent = '已查看 ✓';
                    card.querySelector('button').disabled = true;
                }
                addCoin(0);
            };

            // 语音输入
            document.getElementById('voiceBtn').addEventListener('click', function() {
                const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
                if (!SpeechRecognition) {
                    showToast('您的浏览器不支持语音输入，请手动输入方案');
                    return;
                }
                const recognition = new SpeechRecognition();
                recognition.lang = 'zh-CN';
                recognition.interimResults = false;
                recognition.start();
                this.textContent = '🎤 聆听中...';
                recognition.onresult = function(event) {
                    const transcript = event.results[0][0].transcript;
                    planText.value += transcript;
                    document.getElementById('voiceBtn').textContent = '🎤 语音输入方案';
                };
                recognition.onerror = function() {
                    document.getElementById('voiceBtn').textContent = '🎤 语音输入方案';
                    showToast('语音识别失败，请重试或手动输入');
                };
                recognition.onend = function() {
                    document.getElementById('voiceBtn').textContent = '🎤 语音输入方案';
                };
            });

            // ============ 页面4：搜集证据 ============
            window.openEvidence = function(type) {
                let html = '';
                switch (type) {
                    case 'book':
                        html = `
                      <h3 style="color:var(--green-700);">📖 权威书籍 · 蚜虫身份信息</h3>
                      <div style="background:#f9fafb;border-radius:14px;padding:14px;margin:10px 0;">
                        <p><strong>《农业昆虫学》记载：</strong></p>
                        <ul style="padding-left:18px;font-size:13px;line-height:1.8;">
                          <li><strong>学名：</strong>蚜虫属半翅目蚜总科（Aphidoidea），全球已知约4400种。</li>
                          <li><strong>体长：</strong>1-2毫米，较大种类可达4毫米。</li>
                          <li><strong>体色：</strong>丰富多样，常见绿、黄、黑、红、棕等色。</li>
                          <li><strong>形态：</strong>身体柔软呈梨形，腹部有一对"腹管"（管状突起），触角较长。</li>
                          <li><strong>繁殖：</strong>孤雌生殖（不需交配即可繁殖），繁殖力极强，条件适宜时数量可迅速暴增。</li>
                        </ul>
                        <p style="margin-top:8px;"><strong>蔬菜蚜虫主要种类：</strong></p>
                        <ul style="padding-left:18px;font-size:13px;line-height:1.8;">
                          <li><strong>桃蚜：</strong>体色多变，寄主广泛，可传播多种植物病毒。</li>
                          <li><strong>萝卜蚜：</strong>体黄绿色，主要危害十字花科蔬菜。</li>
                          <li><strong>甘蓝蚜：</strong>体灰绿色，喜在叶面光滑的十字花科蔬菜上取食。</li>
                        </ul>
                        <p style="margin-top:8px;font-size:12px;color:var(--gray-500);">📋 参考来源：《农业昆虫学》《植物病理学》</p>
                      </div>`;
                        break;
                    case 'image':
                        html = `
                      <h3 style="color:var(--green-700);">🖼️ 图像资料 & AR模型</h3>
                      <div style="background:#f9fafb;border-radius:14px;padding:14px;margin:10px 0;">
                        <p><strong>📷 蚜虫参考照片：</strong></p>
                        <p style="font-size:13px;">请参考课本图册中蚜虫的近距离照片，注意观察：</p>
                        <ul style="padding-left:18px;font-size:13px;line-height:1.8;">
                          <li>蚜虫群集在叶片背面的状态</li>
                          <li>有翅蚜与无翅蚜的形态对比</li>
                          <li>蚜虫蜕皮（白色皮壳）</li>
                          <li>蚜虫与蚂蚁共生的场景</li>
                          <li>蚜虫危害后叶片卷曲的症状</li>
                        </ul>
                        <p style="margin-top:10px;"><strong>🥽 三维AR模型使用指南：</strong></p>
                        <p style="font-size:13px;background:#fef3c7;padding:10px;border-radius:10px;">
                          📱 到<strong>平板主页</strong>点开<strong>绿色图标"AR昆虫观察"</strong>，将摄像头对准叶片或课本上的蚜虫图片，即可看到放大的三维蚜虫模型，可以旋转、缩放观察蚜虫的各个部位！
                        </p>
                      </div>`;
                        break;
                    case 'ai':
                        html = `
                      <h3 style="color:var(--green-700);">🤖 AI专家沟通</h3>
                      <div style="background:#f9fafb;border-radius:14px;padding:14px;margin:10px 0;">
                        <p><strong>📞 AI电话沟通指南：</strong></p>
                        <p style="font-size:13px;background:#fef3c7;padding:10px;border-radius:10px;">
                          到<strong>平板主页</strong>点开对应图标，选择<strong>"蔬菜病虫害防治专家"</strong>（厦门本土专家AI），你可以选择和他进行语音通话或文字交流。
                        </p>
                        <p style="margin-top:10px;"><strong>💬 或直接在此文字对话：</strong></p>
                        <p style="font-size:12px;color:var(--gray-500);">输入你的问题，专家会为你解答（支持跳转外部智能体）</p>
                      </div>
                      <div class="chat-window" id="chatWindow4">
                        <div class="chat-bubble chat-bot">👨‍🌾 你好！我是厦门本土"蔬菜病虫害防治专家"。关于蚜虫和白菜病害，你有什么想了解的？</div>
                      </div>
                      <div style="display:flex;gap:6px;margin-top:8px;">
                        <input type="text" id="aiInput4" placeholder="输入你的问题…" style="flex:1;">
                        <button class="btn btn-primary btn-sm" onclick="sendAIMessage()">发送</button>
                      </div>
                      <p style="margin-top:10px;font-size:12px;color:var(--gray-500);">
                        或跳转到完整AI专家页面：
                        <a href="https://mbd.baidu.com/ma/s/l8aLkR2o" target="_blank" style="color:var(--green-600);font-weight:600;">点此打开百度智能体专家 →</a>
                      </p>`;
                        break;
                    case 'observe':
                        html = `
                      <h3 style="color:var(--green-700);">🔬 实物观察指南</h3>
                      <div style="background:#f9fafb;border-radius:14px;padding:14px;margin:10px 0;">
                        <p><strong>用放大镜观察蚜虫的步骤：</strong></p>
                        <ol style="padding-left:20px;font-size:13px;line-height:2;">
                          <li>取一片被蚜虫侵害的白菜叶片</li>
                          <li><strong>翻看叶片背面</strong>，寻找群居的小虫</li>
                          <li>用<strong>10倍放大镜</strong>仔细观察虫体颜色、大小、有无翅膀</li>
                          <li>观察<strong>腹管</strong>（腹部两侧的管状突起）——这是蚜虫的重要特征</li>
                          <li>触摸叶片表面，感受<strong>蜜露的黏腻感</strong></li>
                          <li>注意观察是否有<strong>蚂蚁</strong>在蚜虫周围活动</li>
                          <li>寻找白色蜕皮壳和蚜虫卵</li>
                        </ol>
                        <p style="margin-top:10px;font-size:13px;background:#fef3c7;padding:10px;border-radius:10px;">
                          <strong>🔎 观察小提示：</strong><br>
                          ① 可用<strong>透明胶带轻轻粘取</strong>叶片背面的蚜虫，贴在白纸上再用放大镜观察。<br>
                          ② 将蚜虫放入<strong>透明小瓶</strong>中，从不同角度观察其形态。<br>
                          ③ 记录观察到的蚜虫数量、颜色、分布位置，绘制简图。<br>
                          ④ 对比健康叶片与受害叶片的差异。
                        </p>
                      </div>`;
                        break;
                }
                openModal(html);
                addCoin(0);
            };

            // AI对话功能
            const expertKnowledge = {
                '蚜虫': '蚜虫属半翅目蚜总科，体长1-2毫米，体色多样。它们用刺吸式口器吸食植物汁液，导致叶片卷曲、发黄。腹部的"腹管"是重要识别特征。',
                '危害': '蚜虫以成蚜、若蚜密集在叶背、茎枝上刺吸汁液，破坏叶肉和叶绿素。苗期叶片受害卷曲、发黄、植株矮缩、生长缓慢，严重时叶片枯死。蚜虫还可传播多种病毒病。',
                '白菜': '蚜虫偏嗜白菜及芥菜型油菜等十字花科蔬菜。被害白菜叶片向下畸形卷缩，植株矮小，影响包心。蚜虫分泌的蜜露会诱发煤污病，阻碍光合作用。',
                '防治': '可采用悬挂黄板诱杀有翅蚜、释放瓢虫和草蛉等天敌、喷洒苦参碱或印楝素等植物源杀虫剂、早期用高压水流冲洗叶片。关键要早发现早处理。',
                '厦门': '厦门春季（3-5月）气温18-25℃，是蚜虫高发期。今年5月上旬厦门气温在18-29℃之间，晴好天气多，非常适合蚜虫繁殖。建议密切关注菜园蚜虫动态。',
                '天气': '根据厦门2025年5月天气数据：5月1日-4日气温在20-29℃之间，多云为主；5月7日-10日气温18-30℃，大多晴朗。这样的温暖天气正适合蚜虫大量繁殖。',
                '观察': '建议用10倍放大镜翻看叶片背面，寻找群居的绿色小虫。蚜虫通常聚集在嫩叶和嫩梢部位。可用透明胶带粘取后贴在白纸上观察。注意区分有翅蚜和无翅蚜。',
                '蜜露': '蜜露是蚜虫排泄的含糖液体，黏腻发亮。蜜露会滴落在下部叶片上，诱发煤污病（黑色霉层），还会吸引蚂蚁。蚂蚁为了保护蜜露来源，会驱赶蚜虫的天敌。',
                '天敌': '蚜虫的主要天敌包括瓢虫（七星瓢虫、异色瓢虫）、草蛉、食蚜蝇、寄生蜂等。一只瓢虫一天可捕食100多只蚜虫。保护和引入天敌是最环保的防治方法。',
                'default': '这是个好问题！建议你结合观察实际叶片、查阅课本资料、以及与其他同学讨论来进一步探究。记住：科学探究需要多方面搜集证据哦！'
            };

            window.sendAIMessage = function() {
                const input = document.getElementById('aiInput4');
                if (!input) return;
                const text = input.value.trim();
                if (!text) return;
                const chatWindow = document.getElementById('chatWindow4');
                if (!chatWindow) return;
                const userBubble = document.createElement('div');
                userBubble.className = 'chat-bubble chat-user';
                userBubble.textContent = '👦 ' + text;
                chatWindow.appendChild(userBubble);
                let reply = expertKnowledge['default'];
                for (const [key, val] of Object.entries(expertKnowledge)) {
                    if (text.includes(key)) { reply = val; break; }
                }
                setTimeout(() => {
                    const botBubble = document.createElement('div');
                    botBubble.className = 'chat-bubble chat-bot';
                    botBubble.textContent = '👨‍🌾 ' + reply;
                    chatWindow.appendChild(botBubble);
                    chatWindow.scrollTop = chatWindow.scrollHeight;
                }, 500);
                input.value = '';
                chatWindow.scrollTop = chatWindow.scrollHeight;
            };

            // ============ 页面5：汇报交流（评价量表） ============
            window.calculateLevel = function() {
                const group = document.getElementById('groupSelect').value;
                const checkboxes = document.querySelectorAll('.rubric-check:checked');
                let totalScore = 0;
                checkboxes.forEach(cb => {
                    totalScore += parseInt(cb.dataset.score || 0);
                });
                const maxScore = 18; // 总分
                let level = '';
                let icon = '';
                let color = '';
                if (totalScore >= 16) {
                    level = '💎 钻石侦探';
                    icon = '💎';
                    color = '#2563eb';
                } else if (totalScore >= 12) {
                    level = '🥇 金牌侦探';
                    icon = '🥇';
                    color = '#d97706';
                } else if (totalScore >= 8) {
                    level = '🥈 银牌侦探';
                    icon = '🥈';
                    color = '#6b7280';
                } else if (totalScore >= 4) {
                    level = '🥉 铜牌侦探';
                    icon = '🥉';
                    color = '#92400e';
                } else {
                    level = '🔍 见习侦探';
                    icon = '🔍';
                    color = '#6b7280';
                }
                const resultEl = document.getElementById('levelResult');
                resultEl.innerHTML = `
                <div style="background:#f9fafb;border-radius:20px;padding:18px;text-align:center;">
                  <p style="font-size:14px;color:var(--gray-500);">${group}</p>
                  <div class="level-badge" style="background:${color}15;color:${color};">
                    ${icon} ${level}
                  </div>
                  <p style="margin-top:8px;font-size:14px;">
                    得分：<strong style="font-size:22px;color:var(--green-700);">${totalScore}</strong> / ${maxScore} 分
                  </p>
                  <div class="prob-bar" style="margin:8px 0;"><div class="prob-fill" style="width:${(totalScore/maxScore)*100}%;background:${color};"></div></div>
                  <p style="font-size:12px;color:var(--gray-500);">剩余侦探币：${detectiveCoins} 🪙</p>
                  <p style="font-size:12px;color:var(--gray-400);margin-top:4px;">评价维度参考《义务教育科学课程标准（2022年版）》</p>
                </div>`;
                document.getElementById('finalCoins').textContent = detectiveCoins;
                updateCoinDisplay();
            };

            // 评价量表实时更新剩余侦探币
            document.getElementById('rubricTable').addEventListener('change', function() {
                updateCoinDisplay();
            });

            // ============ 初始化 ============
            updateCoinDisplay();
            navigateTo('page1');

            // 键盘快捷键
            document.addEventListener('keydown', function(e) {
                if (e.key === 'Escape') closeModal();
            });

            console.log('🌱 菜园奇遇记 · 科学侦探探究已就绪');
            console.log('  📸 页面2：拍照识别（蚜虫大概率）');
            console.log('  📋 页面3：设计方案（语音输入+提示卡片）');
            console.log('  🔍 页面4：搜集证据（书籍/图像/AI/观察）');
            console.log('  🏆 页面5：课标评价量表 · 自动积分');
        })();
    </script>
</body>
</html>
