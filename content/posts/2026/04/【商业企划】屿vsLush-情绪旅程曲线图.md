+++
date = '2026-04-11T18:03:43+08:00'
draft = false
title = '【商业企划】屿vsLush 情绪旅程曲线图'
tags = ["屿"]
categories = ["奥赛罗拾光"]
summary = "日常生活中的一座孤岛，5分钟的绝对自我时刻。" 
+++

## 画出可交互的情绪曲线图（HTML/JS版本，可嵌入PPT）

{{< figure 
    src="/images/posts/2026/04/“屿”的情绪旅程曲线图/情绪旅程曲线图对比.png"
    title="情绪旅程曲线图对比：屿 vs Lush"
>}}

以下是“屿 vs Lush”可交互情绪曲线图的完整HTML代码。它是一个独立的网页文件，可直接在浏览器中运行，也支持嵌入PPT（Windows版可通过Web Browser控件加载）。

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>屿 vs Lush - 情绪旅程曲线图 | 交互式体验设计</title>
    <!-- 引入 Chart.js 轻量图表库 -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <!-- 引入 Font Awesome 6 (免费图标库) -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #f2efe9 0%, #e8e2d8 100%);
            font-family: 'Inter', 'Segoe UI', 'Roboto', system-ui, -apple-system, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 2rem;
        }

        /* 主卡片风格：侘寂 / 极简 */
        .chart-container {
            max-width: 1300px;
            width: 100%;
            background: #fefaf5;
            border-radius: 2rem;
            box-shadow: 0 20px 35px -12px rgba(0,0,0,0.2), 0 1px 2px rgba(0,0,0,0.05);
            overflow: hidden;
            transition: all 0.2s ease;
        }

        /* 头部品牌区 */
        .hero {
            padding: 2rem 2.5rem 1rem 2.5rem;
            border-bottom: 1px solid #e2d9cf;
        }

        .brand-badge {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .title-section h1 {
            font-size: 1.9rem;
            font-weight: 500;
            letter-spacing: -0.3px;
            color: #2c2a27;
            margin-bottom: 0.4rem;
        }

        .title-section h1 i {
            color: #b87c4f;
            font-size: 1.8rem;
            margin-right: 8px;
        }

        .sub {
            color: #7f6e5d;
            font-size: 0.9rem;
            font-weight: 400;
            border-left: 3px solid #c2a383;
            padding-left: 12px;
            margin-top: 6px;
        }

        .legend-buttons {
            display: flex;
            gap: 2rem;
            background: #f4efe8;
            padding: 0.5rem 1.2rem;
            border-radius: 60px;
        }

        .legend-lush {
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: 500;
            color: #cf6f4a;
        }

        .legend-yu {
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: 500;
            color: #5b7b6e;
        }

        .dot-lush {
            width: 20px;
            height: 20px;
            background: #e58c6a;
            border-radius: 20px;
            box-shadow: 0 0 0 2px #fbe9e2;
        }

        .dot-yu {
            width: 20px;
            height: 20px;
            background: #6e9f8c;
            border-radius: 20px;
            box-shadow: 0 0 0 2px #e0f0ea;
        }

        /* 图表区域 */
        .graph-wrapper {
            padding: 1.5rem 2rem 0.5rem 2rem;
            position: relative;
        }

        canvas {
            max-height: 460px;
            width: 100%;
            cursor: pointer;
        }

        /* 控制栏：交互提示与重置 */
        .interaction-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.5rem 2rem 0 2rem;
            flex-wrap: wrap;
        }

        .tooltip-hint {
            background: #e9e1d7;
            border-radius: 30px;
            padding: 6px 14px;
            font-size: 0.75rem;
            color: #5f5346;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .tooltip-hint i {
            font-size: 0.8rem;
        }

        .reset-btn {
            background: none;
            border: 1px solid #cfc3b6;
            padding: 5px 14px;
            border-radius: 30px;
            font-size: 0.75rem;
            color: #8b765e;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 500;
        }

        .reset-btn:hover {
            background: #e3d9ce;
            border-color: #b2947a;
            color: #4f3e2e;
        }

        /* 阶段解释卡 (动态高亮) */
        .stages-panel {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            gap: 0.8rem;
            padding: 1.5rem 2rem 2rem 2rem;
            border-top: 1px solid #e9e0d6;
            margin-top: 0.5rem;
        }

        .stage-card {
            flex: 1;
            min-width: 100px;
            background: #fefaf5;
            border-radius: 1.2rem;
            padding: 0.8rem 0.6rem;
            text-align: center;
            transition: all 0.2s ease;
            border: 1px solid #ede3d8;
            cursor: default;
        }

        .stage-card.active {
            background: #f6efe8;
            border-left: 4px solid #b87c4f;
            box-shadow: 0 4px 8px rgba(0,0,0,0.02);
            transform: translateY(-2px);
        }

        .stage-name {
            font-weight: 600;
            font-size: 0.85rem;
            letter-spacing: 0.3px;
            color: #4b3f33;
        }

        .stage-values {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-top: 8px;
            font-size: 0.7rem;
            font-weight: 500;
        }

        .lush-val {
            color: #cf6f4a;
        }

        .yu-val {
            color: #5b7b6e;
        }

        .insight {
            font-size: 0.7rem;
            margin-top: 8px;
            color: #8f7b66;
            border-top: 1px dashed #e2cfbd;
            padding-top: 6px;
        }

        /* 底部金句 */
        .quote-footer {
            background: #f3ede6;
            padding: 1rem 2rem;
            text-align: center;
            font-size: 0.85rem;
            font-style: italic;
            color: #4e4238;
            border-top: 1px solid #e4d9ce;
            display: flex;
            justify-content: center;
            gap: 2rem;
            flex-wrap: wrap;
        }

        .quote-item {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        hr {
            margin: 0 2rem;
            border-color: #e7dfd5;
        }

        @media (max-width: 780px) {
            body {
                padding: 1rem;
            }
            .hero {
                padding: 1.2rem;
            }
            .graph-wrapper {
                padding: 1rem;
            }
            .stages-panel {
                padding: 1rem;
            }
            .stage-values {
                flex-direction: column;
                gap: 0.3rem;
            }
            .legend-buttons {
                margin-top: 0.8rem;
            }
        }
    </style>
</head>
<body>

<div class="chart-container">
    <div class="hero">
        <div class="brand-badge">
            <div class="title-section">
                <h1><i class="fas fa-water"></i> 屿 · 情绪旅程地图</h1>
                <div class="sub">感知锚定 × 内感受闭环 × 文化叙事 × 稀缺锁定 —— 与Lush的神经劫持对比</div>
            </div>
            <div class="legend-buttons">
                <div class="legend-lush"><span class="dot-lush"></span> Lush (多巴胺追逐)</div>
                <div class="legend-yu"><span class="dot-yu"></span> 屿 (血清素归属)</div>
            </div>
        </div>
    </div>

    <div class="graph-wrapper">
        <canvas id="emotionChart" width="1000" height="400" style="width:100%; height:auto; max-height:450px"></canvas>
    </div>

    <div class="interaction-bar">
        <div class="tooltip-hint"><i class="fas fa-hand-pointer"></i> 悬停或点击图表曲线 → 查看详细情绪锚点</div>
        <button class="reset-btn" id="resetHighlightBtn"><i class="fas fa-undo-alt"></i> 重置高亮</button>
    </div>

    <!-- 阶段卡片：动态绑定高亮 + 显示具体数值 -->
    <div class="stages-panel" id="stagesPanel">
        <!-- 动态js生成也可以，但为了清晰直接硬编码但数据绑定由js控制高亮 -->
    </div>

    <div class="quote-footer">
        <div class="quote-item"><i class="fas fa-candy-cane" style="color:#cf6f4a;"></i> Lush：像糖，瞬间快乐</div>
        <div class="quote-item"><i class="fas fa-leaf" style="color:#6e9f8c;"></i> 屿：像茶，回甘悠长</div>
        <div class="quote-item"><i class="fas fa-chart-line"></i> 多巴胺驱动追逐 · 血清素驱动归属</div>
    </div>
</div>

<script>
    // 阶段定义：严格按照旅程地图 注意 -> 兴趣 -> 首次使用 -> 使用中 -> 使用后 -> 30分钟后
    const stages = ["注意", "兴趣", "首次使用", "使用中", "使用后", "30分钟后"];
    // Lush 情绪唤醒度 (1-10)
    const lushScores = [9, 8, 9, 7, 5, 3];
    // 屿 情绪唤醒度 (注意阶段低开，首次使用有4→8的变化，但图表上体现为单个数值，我们取峰值后的体验值8，使用中9，使用后7，30min后6)
    // 为了让曲线更精准，屿的首次使用取情绪反转后的峰值感 8 (代表努力后奖励的峰值)。 注意点：10秒延迟低点（4）单独用小提示，曲线代表最终体验，符合叙事。
    // 但我们可用 tooltip 补充细节。为呈现曲线差异，屿数值 = [5, 7, 8, 9, 7, 6]
    const yuScores = [5, 7, 8, 9, 7, 6];
    
    // 额外叙事映射表 (劫持点描述)
    const narrativeMap = {
        "注意": { lush: "视觉炸裂 / 糖果感 → 多巴胺启动", yu: "低饱和斑驳 / 河卵石质感 → 审美好奇唤醒" },
        "兴趣": { lush: "复合花果香冲击 → 嗅觉记忆快速编码", yu: "冷杉基底香 → 侦探模式: '这个熟悉的味道是什么?'" },
        "首次使用": { lush: "零门槛起泡 / 蓬松大泡 → 即时满足", yu: "10秒激活仪式 → 努力→奖励闭环，用户亲手创造泡沫" },
        "使用中": { lush: "清爽洗净，蓬松触感 → 功能清洁", yu: "乳霜泡沫包裹 / 五感打通 → 触觉验证孤岛叙事" },
        "使用后": { lush: "香味快速消散，无残留感 → 记忆中断", yu: "皮肤海盐壳 + 冷杉淡香 → 叙事延续30分钟" },
        "30分钟后": { lush: "几乎无痕，情绪基线回落", yu: "偶尔闻到冷杉/海盐 → 提醒'你还在屿上'，血清素满足" }
    };
    
    // 额外关键劫持点描述 (用于点击/悬停)
    const extraInsight = {
        "首次使用": "✨ 屿的设计精髓：10秒延迟制造‘仪式感’，情绪短暂下挫后飙升至8分，形成比Lush更深的记忆烙印。",
        "使用中": "🌊 屿峰值9分：乳霜泡沫+冷杉海盐气味+视觉斑驳 → 内感受闭环彻底激活",
        "30分钟后": "🏝️ 屿仍维持6分唤醒：皮肤膜感是‘岛’的物理证据，复购由归属感驱动。"
    };
    
    let chart; // 图表实例
    let currentActiveIndex = -1;
    
    // 渲染阶段卡片
    function renderStageCards() {
        const panel = document.getElementById("stagesPanel");
        if (!panel) return;
        panel.innerHTML = "";
        stages.forEach((stage, idx) => {
            const lushVal = lushScores[idx];
            const yuVal = yuScores[idx];
            const card = document.createElement("div");
            card.className = "stage-card";
            card.setAttribute("data-stage-idx", idx);
            card.innerHTML = `
                <div class="stage-name">${stage}</div>
                <div class="stage-values">
                    <span class="lush-val">🍬 Lush ${lushVal}</span>
                    <span class="yu-val">🌿 屿 ${yuVal}</span>
                </div>
                <div class="insight">${getShortInsight(stage, idx)}</div>
            `;
            card.addEventListener("click", (e) => {
                e.stopPropagation();
                highlightStage(idx);
                // 同时高亮图表数据点（通过chart tooltip模拟或手动更新dataset？直接调用图表内置高亮不够直观，我们更新卡片样式并显示额外信息）
                showStageDetail(idx);
            });
            panel.appendChild(card);
        });
    }
    
    function getShortInsight(stage, idx) {
        if (stage === "首次使用") return "⏳ 10秒延迟 → 努力即奖励";
        if (stage === "使用中") return "🧼 乳霜泡沫 + 冷杉基底";
        if (stage === "30分钟后") return "🌫️ 皮肤膜感延续叙事";
        if (stage === "注意") return "🎨 屿：低饱和孤岛美学";
        if (stage === "兴趣") return "👃 冷杉指纹 → 跨产品劫持";
        if (stage === "使用后") return "🐚 海盐壳残留，30分钟回甘";
        return "";
    }
    
    // 高亮卡片
    function highlightStage(index) {
        // 重置所有卡片active样式
        const cards = document.querySelectorAll(".stage-card");
        cards.forEach((card, i) => {
            if (i === index) {
                card.classList.add("active");
            } else {
                card.classList.remove("active");
            }
        });
        currentActiveIndex = index;
        // 可选：同时触发表格tooltip模拟显示
    }
    
    // 显示更详细的信息 (使用弹窗/控制台? 优雅地展示在图表旁或者一个小浮层, 为了不侵入，采用浏览器自带alert风格太硬，改用临时tooltip浮层)
    // 创建轻提示浮层
    let toastEl = null;
    function showStageDetail(index) {
        const stage = stages[index];
        const lushDesc = narrativeMap[stage]?.lush || "";
        const yuDesc = narrativeMap[stage]?.yu || "";
        let special = extraInsight[stage] || "";
        const message = `【${stage}阶段】\n🔴 Lush: ${lushDesc}\n🟢 屿: ${yuDesc}\n${special ? "✨ " + special : ""}`;
        
        // 创建临时toast
        if (toastEl) toastEl.remove();
        toastEl = document.createElement("div");
        toastEl.style.position = "fixed";
        toastEl.style.bottom = "30px";
        toastEl.style.left = "50%";
        toastEl.style.transform = "translateX(-50%)";
        toastEl.style.backgroundColor = "#2c2a27";
        toastEl.style.color = "#f3ede6";
        toastEl.style.padding = "12px 20px";
        toastEl.style.borderRadius = "40px";
        toastEl.style.fontSize = "0.8rem";
        toastEl.style.maxWidth = "340px";
        toastEl.style.textAlign = "center";
        toastEl.style.zIndex = "1000";
        toastEl.style.boxShadow = "0 8px 18px rgba(0,0,0,0.2)";
        toastEl.style.backdropFilter = "blur(4px)";
        toastEl.style.fontWeight = "500";
        toastEl.style.border = "1px solid #8f7b66";
        toastEl.innerHTML = `<i class="fas fa-chart-line"></i> ${message.replace(/\n/g, '<br>')}`;
        document.body.appendChild(toastEl);
        setTimeout(() => {
            if (toastEl) toastEl.style.opacity = "0";
            setTimeout(() => { if(toastEl) toastEl.remove(); toastEl = null; }, 300);
        }, 4000);
    }
    
    // 初始化图表 (Chart.js)
    function initChart() {
        const ctx = document.getElementById('emotionChart').getContext('2d');
        chart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: stages,
                datasets: [
                    {
                        label: 'Lush 情绪唤醒度',
                        data: lushScores,
                        borderColor: '#e58c6a',
                        backgroundColor: 'rgba(229, 140, 106, 0.08)',
                        borderWidth: 3,
                        pointRadius: 5,
                        pointHoverRadius: 8,
                        pointBackgroundColor: '#cf6f4a',
                        pointBorderColor: '#fff',
                        pointBorderWidth: 2,
                        tension: 0.25,
                        fill: false,
                        pointStyle: 'circle'
                    },
                    {
                        label: '屿 情绪唤醒度',
                        data: yuScores,
                        borderColor: '#6e9f8c',
                        backgroundColor: 'rgba(110, 159, 140, 0.05)',
                        borderWidth: 3,
                        pointRadius: 5,
                        pointHoverRadius: 8,
                        pointBackgroundColor: '#5b7b6e',
                        pointBorderColor: '#fff',
                        pointBorderWidth: 2,
                        tension: 0.25,
                        fill: false,
                        pointStyle: 'rectRounded'
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: true,
                interaction: {
                    mode: 'index',
                    intersect: false,
                },
                plugins: {
                    tooltip: {
                        backgroundColor: '#2c2a27',
                        titleColor: '#f0e5d8',
                        bodyColor: '#ddd0c0',
                        borderColor: '#b2947a',
                        borderWidth: 1,
                        callbacks: {
                            label: function(context) {
                                let label = context.dataset.label || '';
                                let val = context.raw;
                                let stageName = stages[context.dataIndex];
                                let extraMsg = "";
                                if (context.datasetIndex === 1 && stageName === "首次使用") {
                                    extraMsg = " (10秒延迟后爆发)";
                                }
                                if (context.datasetIndex === 1 && stageName === "使用中") {
                                    extraMsg = " ★ 峰值：乳霜泡沫+膜感";
                                }
                                return `${label}: ${val}/10${extraMsg}`;
                            },
                            afterBody: function(tooltipItems) {
                                const idx = tooltipItems[0].dataIndex;
                                const stage = stages[idx];
                                if (stage === "首次使用") return "屿·仪式感: 努力10秒→奖励泡沫";
                                if (stage === "使用后") return "屿·皮肤海盐壳延续体验";
                                return narrativeMap[stage]?.yu || "";
                            }
                        },
                    },
                    legend: {
                        position: 'top',
                        align: 'end',
                        labels: {
                            boxWidth: 14,
                            font: { size: 12, weight: '500' },
                            color: '#5e5346'
                        }
                    }
                },
                scales: {
                    y: {
                        title: {
                            display: true,
                            text: '情绪唤醒度 (1-10)',
                            color: '#8f7b66',
                            font: { size: 11 }
                        },
                        min: 1,
                        max: 10,
                        grid: { color: '#ede0d3', drawBorder: true },
                        ticks: { stepSize: 1, color: '#8f7862' }
                    },
                    x: {
                        title: {
                            display: true,
                            text: '用户旅程阶段',
                            color: '#8f7b66',
                            font: { size: 11 }
                        },
                        ticks: { color: '#6b5a48', fontWeight: '500' },
                        grid: { display: false }
                    }
                },
                onClick: (event, activeElements) => {
                    if (activeElements.length > 0) {
                        const datasetIndex = activeElements[0].datasetIndex;
                        const index = activeElements[0].index;
                        if (datasetIndex === 0 || datasetIndex === 1) {
                            highlightStage(index);
                            showStageDetail(index);
                        }
                    }
                },
                onHover: (event, chartElement) => {
                    if (chartElement && chartElement.length) {
                        document.body.style.cursor = 'pointer';
                    } else {
                        document.body.style.cursor = 'default';
                    }
                }
            }
        });
    }
    
    // 额外在图表上创建动态注释标记: 用原生方法在canvas上方加一个浮动小标记（象征10秒延迟点），由于canvas覆盖，更优雅的方式是在图表旁加标注。
    // 我们增加一个浮动提示元素挂在graph-wrapper内
    function addCustomAnnotation() {
        const wrapper = document.querySelector('.graph-wrapper');
        if (!wrapper) return;
        const marker = document.createElement('div');
        marker.style.position = 'relative';
        marker.style.float = 'right';
        marker.style.marginTop = '-30px';
        marker.style.fontSize = '0.7rem';
        marker.style.background = '#f0e7de';
        marker.style.padding = '2px 12px';
        marker.style.borderRadius = '50px';
        marker.style.display = 'inline-block';
        marker.style.color = '#b87c4f';
        marker.innerHTML = '<i class="fas fa-hourglass-half"></i> 屿·10秒仪式延迟区';
        marker.style.width = 'fit-content';
        wrapper.appendChild(marker);
        
        // 增加一个微妙的引导
        const subNote = document.createElement('div');
        subNote.style.textAlign = 'right';
        subNote.style.fontSize = '0.68rem';
        subNote.style.color = '#aa9986';
        subNote.style.marginTop = '5px';
        subNote.innerHTML = '※ 点击曲线或下方卡片，查看“内感受闭环”劫持点';
        wrapper.appendChild(subNote);
    }
    
    // 重置高亮
    function resetHighlights() {
        const cards = document.querySelectorAll(".stage-card");
        cards.forEach(card => card.classList.remove("active"));
        currentActiveIndex = -1;
        if (toastEl) toastEl.remove();
        // 也可以显示一个简短重置提示
        const tempTip = document.createElement("div");
        tempTip.innerText = "✓ 高亮已重置，可重新探索情绪曲线";
        tempTip.style.position = "fixed";
        tempTip.style.bottom = "20px";
        tempTip.style.left = "20px";
        tempTip.style.backgroundColor = "#5b7b6e";
        tempTip.style.color = "white";
        tempTip.style.padding = "6px 14px";
        tempTip.style.borderRadius = "40px";
        tempTip.style.fontSize = "0.7rem";
        tempTip.style.zIndex = "999";
        document.body.appendChild(tempTip);
        setTimeout(() => tempTip.remove(), 1500);
    }
    
    // 初始化所有
    function init() {
        renderStageCards();
        initChart();
        addCustomAnnotation();
        const resetBtn = document.getElementById("resetHighlightBtn");
        if (resetBtn) resetBtn.addEventListener("click", resetHighlights);
        
        // 自动默认展示第一个阶段引导（可选，但为了体验不自动弹窗）
        // 给首次使用者一个小提示
        setTimeout(() => {
            const hint = document.querySelector(".tooltip-hint");
            if (hint) {
                // 简单闪烁效果
                hint.style.transition = "0.2s";
                hint.style.backgroundColor = "#e2cfbd";
                setTimeout(() => { if(hint) hint.style.backgroundColor = "#e9e1d7"; }, 600);
            }
        }, 800);
    }
    
    init();
</script>
</body>
</html>
