<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Growth Garden — PvP Арена</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #10b981;
            --secondary: #34d399;
            --accent: #f59e0b;
            --danger: #ef4444;
            --info: #3b82f6;
            --bg: #0f172a;
            --surface: rgba(30, 41, 59, 0.8);
            --text: #f1f5f9;
            --text-muted: #94a3b8;
            --enemy: #f43f5e;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            color: var(--text);
            min-height: 100vh;
            overflow-x: hidden;
        }

        .app-container {
            max-width: 480px;
            margin: 0 auto;
            padding: 20px;
            min-height: 100vh;
            position: relative;
        }

        /* Header */
        .header {
            text-align: center;
            margin-bottom: 20px;
            animation: fadeIn 0.8s ease-out;
            position: relative;
        }

        .logo {
            font-size: 28px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 8px;
        }

        .subtitle {
            color: var(--text-muted);
            font-size: 14px;
        }

        .pvp-badge {
            position: absolute;
            top: 0;
            right: 0;
            background: linear-gradient(135deg, var(--danger), #e11d48);
            color: white;
            font-size: 11px;
            font-weight: 800;
            padding: 4px 10px;
            border-radius: 12px;
            animation: pulse 2s infinite;
            display: none;
        }

        .pvp-badge.active {
            display: block;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        /* Navigation Tabs */
        .nav-tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
            background: var(--surface);
            padding: 4px;
            border-radius: 16px;
            backdrop-filter: blur(10px);
        }

        .nav-tab {
            flex: 1;
            padding: 12px;
            text-align: center;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            font-size: 14px;
            transition: all 0.3s;
            color: var(--text-muted);
            position: relative;
        }

        .nav-tab.active {
            background: var(--primary);
            color: white;
            box-shadow: 0 4px 15px rgba(16, 185, 129, 0.3);
        }

        .nav-tab[data-badge]::after {
            content: attr(data-badge);
            position: absolute;
            top: -5px;
            right: 5px;
            background: var(--danger);
            color: white;
            font-size: 10px;
            padding: 2px 6px;
            border-radius: 10px;
            font-weight: 800;
        }

        /* Screens */
        .screen {
            display: none;
            animation: fadeIn 0.5s;
        }

        .screen.active {
            display: block;
        }

        /* Solo Mode (Original) */
        .garden-container {
            background: var(--surface);
            border-radius: 24px;
            padding: 30px;
            margin-bottom: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
            overflow: hidden;
            height: 400px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-end;
        }

        .sky {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 60%;
            background: linear-gradient(to bottom, #1e293b 0%, transparent 100%);
            z-index: 1;
        }

        .stars {
            position: absolute;
            top: 20px;
            left: 20px;
            right: 20px;
            height: 100px;
        }

        .star {
            position: absolute;
            width: 2px;
            height: 2px;
            background: white;
            border-radius: 50%;
            animation: twinkle 3s infinite;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 0.3; }
            50% { opacity: 1; }
        }

        .tree-wrapper {
            position: relative;
            z-index: 2;
            transition: all 0.5s ease;
        }

        .tree {
            position: relative;
            transform-origin: bottom center;
            transition: transform 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        .trunk {
            width: 20px;
            height: 100px;
            background: linear-gradient(to right, #4a3728, #6b4c3a);
            margin: 0 auto;
            border-radius: 0 0 4px 4px;
            position: relative;
            transition: height 0.5s ease;
        }

        .foliage {
            width: 120px;
            height: 120px;
            background: radial-gradient(circle at 30% 30%, var(--secondary), var(--primary));
            border-radius: 50%;
            position: absolute;
            bottom: 80px;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 10px 30px rgba(16, 185, 129, 0.3);
            transition: all 0.5s ease;
            animation: sway 4s ease-in-out infinite;
        }

        .foliage::before, .foliage::after {
            content: '';
            position: absolute;
            background: inherit;
            border-radius: 50%;
        }

        .foliage::before {
            width: 80px;
            height: 80px;
            top: -20px;
            left: -20px;
        }

        .foliage::after {
            width: 70px;
            height: 70px;
            top: -10px;
            right: -20px;
        }

        @keyframes sway {
            0%, 100% { transform: translateX(-50%) rotate(-2deg); }
            50% { transform: translateX(-50%) rotate(2deg); }
        }

        .ground {
            width: 200px;
            height: 40px;
            background: radial-gradient(ellipse at center, rgba(16, 185, 129, 0.3), transparent);
            border-radius: 50%;
            position: absolute;
            bottom: 0;
            z-index: 1;
        }

        /* Tree Stages */
        .tree.stage-1 .trunk { height: 40px; width: 8px; }
        .tree.stage-1 .foliage { width: 40px; height: 40px; bottom: 30px; opacity: 0.7; }

        .tree.stage-2 .trunk { height: 60px; width: 12px; }
        .tree.stage-2 .foliage { width: 70px; height: 70px; bottom: 50px; }

        .tree.stage-3 .trunk { height: 80px; width: 16px; }
        .tree.stage-3 .foliage { width: 100px; height: 100px; bottom: 70px; }

        .tree.stage-4 .trunk { height: 100px; width: 20px; }
        .tree.stage-4 .foliage { width: 130px; height: 130px; bottom: 90px; }

        .tree.stage-5 .trunk { height: 130px; width: 24px; }
        .tree.stage-5 .foliage { width: 160px; height: 160px; bottom: 120px; box-shadow: 0 0 40px rgba(16, 185, 129, 0.5); }

        .fruit {
            position: absolute;
            width: 12px;
            height: 12px;
            background: var(--accent);
            border-radius: 50%;
            box-shadow: 0 0 10px rgba(245, 158, 11, 0.6);
            animation: float 3s ease-in-out infinite;
            display: none;
        }

        .tree.stage-3 .fruit:nth-child(1) { display: block; top: 20px; left: 30%; animation-delay: 0s; }
        .tree.stage-3 .fruit:nth-child(2) { display: block; top: 40px; right: 30%; animation-delay: 1s; }
        .tree.stage-4 .fruit:nth-child(3) { display: block; top: 10px; left: 50%; animation-delay: 2s; }
        .tree.stage-5 .fruit:nth-child(4) { display: block; top: 60px; left: 20%; animation-delay: 0.5s; }
        .tree.stage-5 .fruit:nth-child(5) { display: block; top: 50px; right: 20%; animation-delay: 1.5s; }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }

        /* Stats Bar */
        .stats-bar {
            display: flex;
            justify-content: space-around;
            margin-bottom: 20px;
            gap: 10px;
        }

        .stat-card {
            background: var(--surface);
            border-radius: 16px;
            padding: 16px;
            flex: 1;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: transform 0.2s;
        }

        .stat-value {
            font-size: 32px;
            font-weight: 800;
            color: var(--primary);
            line-height: 1;
            margin-bottom: 4px;
        }

        .stat-label {
            font-size: 12px;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        /* PvP Styles */
        .pvp-lobby {
            background: var(--surface);
            border-radius: 24px;
            padding: 24px;
            margin-bottom: 20px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .lobby-header {
            text-align: center;
            margin-bottom: 24px;
        }

        .lobby-title {
            font-size: 24px;
            font-weight: 800;
            margin-bottom: 8px;
            background: linear-gradient(135deg, var(--danger), #fb7185);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .lobby-subtitle {
            color: var(--text-muted);
            font-size: 14px;
        }

        .duel-options {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 20px;
        }

        .duel-card {
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 16px;
        }

        .duel-card:hover {
            border-color: var(--danger);
            background: rgba(244, 63, 94, 0.1);
            transform: translateY(-2px);
        }

        .duel-icon {
            font-size: 32px;
        }

        .duel-info {
            flex: 1;
        }

        .duel-name {
            font-weight: 700;
            margin-bottom: 4px;
        }

        .duel-desc {
            font-size: 13px;
            color: var(--text-muted);
        }

        .duel-reward {
            background: linear-gradient(135deg, var(--accent), #fbbf24);
            color: #000;
            padding: 6px 12px;
            border-radius: 20px;
            font-weight: 700;
            font-size: 12px;
        }

        /* PvP Arena */
        .pvp-arena {
            display: none;
        }

        .pvp-arena.active {
            display: block;
        }

        .battle-header {
            background: linear-gradient(135deg, rgba(244, 63, 94, 0.2), rgba(225, 29, 72, 0.2));
            border: 1px solid rgba(244, 63, 94, 0.3);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 20px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .battle-title {
            font-size: 20px;
            font-weight: 800;
            margin-bottom: 8px;
            color: #fb7185;
        }

        .battle-timer {
            font-size: 32px;
            font-weight: 800;
            font-family: 'Courier New', monospace;
            color: var(--accent);
            text-shadow: 0 0 20px rgba(245, 158, 11, 0.5);
        }

        .vs-divider {
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 20px 0;
            position: relative;
        }

        .vs-line {
            flex: 1;
            height: 2px;
            background: linear-gradient(90deg, var(--primary), transparent);
        }

        .vs-line.right {
            background: linear-gradient(90deg, transparent, var(--enemy));
        }

        .vs-text {
            font-size: 24px;
            font-weight: 900;
            color: var(--accent);
            margin: 0 20px;
            animation: pulse 1.5s infinite;
        }

        .battle-field {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
            margin-bottom: 20px;
        }

        .player-side {
            background: var(--surface);
            border-radius: 20px;
            padding: 16px;
            text-align: center;
            border: 2px solid transparent;
            transition: all 0.3s;
            position: relative;
        }

        .player-side.me {
            border-color: var(--primary);
            box-shadow: 0 0 20px rgba(16, 185, 129, 0.2);
        }

        .player-side.enemy {
            border-color: var(--enemy);
            box-shadow: 0 0 20px rgba(244, 63, 94, 0.2);
        }

        .player-side.winner {
            animation: winnerPulse 1s infinite;
            border-color: var(--accent);
        }

        @keyframes winnerPulse {
            0%, 100% { box-shadow: 0 0 20px rgba(245, 158, 11, 0.4); }
            50% { box-shadow: 0 0 40px rgba(245, 158, 11, 0.8); }
        }

        .player-avatar {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            margin: 0 auto 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            background: var(--surface);
            border: 3px solid var(--primary);
        }

        .player-side.enemy .player-avatar {
            border-color: var(--enemy);
        }

        .player-name {
            font-weight: 700;
            margin-bottom: 4px;
        }

        .player-streak {
            font-size: 24px;
            font-weight: 800;
            color: var(--primary);
            margin-bottom: 8px;
        }

        .player-side.enemy .player-streak {
            color: var(--enemy);
        }

        .health-bar {
            height: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 8px;
        }

        .health-fill {
            height: 100%;
            background: var(--primary);
            transition: width 0.5s ease;
        }

        .player-side.enemy .health-fill {
            background: var(--enemy);
        }

        /* Battle Actions */
        .battle-actions {
            display: flex;
            gap: 12px;
            margin-bottom: 20px;
        }

        .battle-btn {
            flex: 1;
            padding: 16px;
            border: none;
            border-radius: 16px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 14px;
        }

        .btn-attack {
            background: linear-gradient(135deg, var(--danger), #e11d48);
            color: white;
            box-shadow: 0 4px 15px rgba(239, 68, 68, 0.3);
        }

        .btn-attack:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(239, 68, 68, 0.4);
        }

        .btn-taunt {
            background: var(--surface);
            color: var(--text);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .btn-taunt:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        /* Taunt Messages */
        .taunt-bubble {
            position: fixed;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%) translateY(20px);
            background: var(--surface);
            padding: 16px 24px;
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            opacity: 0;
            transition: all 0.3s;
            z-index: 100;
            max-width: 90%;
            text-align: center;
            font-weight: 600;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
        }

        .taunt-bubble.show {
            opacity: 1;
            transform: translateX(-50%) translateY(0);
        }

        .taunt-bubble::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            border-width: 10px 10px 0;
            border-style: solid;
            border-color: var(--surface) transparent transparent;
        }

        /* Code Input */
        .code-input-group {
            display: flex;
            gap: 8px;
            margin-bottom: 16px;
        }

        .code-input {
            flex: 1;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.1);
            color: white;
            padding: 16px;
            border-radius: 12px;
            font-size: 18px;
            text-align: center;
            font-weight: 700;
            letter-spacing: 4px;
            text-transform: uppercase;
        }

        .code-input:focus {
            outline: none;
            border-color: var(--danger);
        }

        /* Share Code */
        .share-code {
            background: rgba(16, 185, 129, 0.1);
            border: 2px dashed var(--primary);
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            margin-bottom: 16px;
        }

        .code-display {
            font-size: 32px;
            font-weight: 800;
            letter-spacing: 8px;
            color: var(--primary);
            margin: 12px 0;
            font-family: 'Courier New', monospace;
        }

        .copy-btn {
            background: var(--primary);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.2s;
        }

        .copy-btn:hover {
            background: var(--secondary);
        }

        /* Leaderboard */
        .leaderboard {
            background: var(--surface);
            border-radius: 20px;
            padding: 20px;
        }

        .leader-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            margin-bottom: 8px;
            transition: all 0.2s;
        }

        .leader-item:hover {
            background: rgba(255, 255, 255, 0.1);
            transform: translateX(5px);
        }

        .leader-rank {
            font-size: 20px;
            font-weight: 800;
            width: 30px;
            text-align: center;
        }

        .leader-rank.gold { color: #ffd700; }
        .leader-rank.silver { color: #c0c0c0; }
        .leader-rank.bronze { color: #cd7f32; }

        .leader-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--surface);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
        }

        .leader-info {
            flex: 1;
        }

        .leader-name {
            font-weight: 600;
            font-size: 14px;
        }

        .leader-score {
            font-size: 12px;
            color: var(--text-muted);
        }

        .leader-wins {
            font-weight: 800;
            color: var(--accent);
        }

        /* Progress Containers */
        .progress-container {
            background: var(--surface);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .progress-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 12px;
            font-size: 14px;
        }

        .progress-bar {
            height: 12px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 6px;
            overflow: hidden;
            position: relative;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 6px;
            transition: width 0.6s ease;
            position: relative;
            overflow: hidden;
        }

        .progress-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: shimmer 2s infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(10px);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .modal.active {
            display: flex;
            animation: fadeIn 0.3s;
        }

        .modal-content {
            background: var(--surface);
            border-radius: 24px;
            padding: 30px;
            max-width: 400px;
            width: 100%;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
            animation: slideUp 0.3s;
        }

        .modal-icon {
            font-size: 64px;
            margin-bottom: 16px;
        }

        .modal-title {
            font-size: 24px;
            font-weight: 800;
            margin-bottom: 8px;
        }

        .modal-text {
            color: var(--text-muted);
            margin-bottom: 24px;
            line-height: 1.5;
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            color: white;
            padding: 14px 28px;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.2s;
            width: 100%;
        }

        .btn-secondary:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        .btn-primary {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border: none;
            border-radius: 16px;
            color: white;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 20px rgba(16, 185, 129, 0.3);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(16, 185, 129, 0.4);
        }

        .btn-primary:disabled {
            background: var(--surface);
            cursor: not-allowed;
            box-shadow: none;
            color: var(--text-muted);
        }

        /* Animations */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Confetti */
        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            pointer-events: none;
            z-index: 9999;
        }

        /* Toast */
        .toast {
            position: fixed;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: var(--surface);
            color: white;
            padding: 16px 24px;
            border-radius: 12px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.3);
            opacity: 0;
            transition: all 0.3s;
            z-index: 100;
            border: 1px solid rgba(255,255,255,0.1);
            font-weight: 600;
        }

        .toast.show {
            transform: translateX(-50%) translateY(0);
            opacity: 1;
        }

        /* Habit Selector */
        .habit-selector {
            display: flex;
            gap: 8px;
            overflow-x: auto;
            margin-bottom: 20px;
            padding-bottom: 10px;
            scrollbar-width: none;
        }

        .habit-selector::-webkit-scrollbar {
            display: none;
        }

        .habit-chip {
            padding: 8px 16px;
            background: var(--surface);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            cursor: pointer;
            white-space: nowrap;
            transition: all 0.2s;
            font-size: 14px;
        }

        .habit-chip.active {
            background: var(--primary);
            border-color: var(--primary);
            color: white;
        }

        /* Responsive */
        @media (max-width: 480px) {
            .app-container {
                padding: 16px;
            }
            
            .battle-field {
                gap: 12px;
            }
        }
    </style>
</head>
<body>

<div class="app-container">
    <header class="header">
        <div class="pvp-badge" id="pvpBadge">PvP Активен</div>
        <h1 class="logo">🌱 Growth Garden</h1>
        <p class="subtitle">Расти вместе с собой • Соревнуйся с друзьями</p>
    </header>

    <!-- Navigation -->
    <div class="nav-tabs">
        <div class="nav-tab active" onclick="switchTab('solo')">🌳 Соло</div>
        <div class="nav-tab" onclick="switchTab('pvp')" id="pvpTab">⚔️ PvP Арена</div>
        <div class="nav-tab" onclick="switchTab('leaderboard')">🏆 Топ</div>
    </div>

    <!-- Solo Screen -->
    <div class="screen active" id="soloScreen">
        <div class="habit-selector" id="habitSelector">
            <div class="habit-chip active" data-habit="smoking">🚭 Курение</div>
            <div class="habit-chip" data-habit="alcohol">🍷 Алкоголь</div>
            <div class="habit-chip" data-habit="sugar">🍬 Сахар</div>
            <div class="habit-chip" data-habit="social">📱 Соцсети</div>
            <div class="habit-chip" data-habit="coffee">☕ Кофеин</div>
        </div>

        <div class="stats-bar">
            <div class="stat-card">
                <div class="stat-value" id="currentStreak">0</div>
                <div class="stat-label">Дней подряд</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="totalDays">0</div>
                <div class="stat-label">Всего</div>
            </div>
            <div class="stat-card">
                <div class="stat-value" id="pvpWins">0</div>
                <div class="stat-label">Побед</div>
            </div>
        </div>

        <div class="garden-container">
            <div class="sky">
                <div class="stars" id="stars"></div>
            </div>
            <div class="ground"></div>
            <div class="tree-wrapper">
                <div class="tree stage-1" id="tree">
                    <div class="foliage">
                        <div class="fruit"></div>
                        <div class="fruit"></div>
                        <div class="fruit"></div>
                        <div class="fruit"></div>
                        <div class="fruit"></div>
                    </div>
                    <div class="trunk"></div>
                </div>
            </div>
        </div>

        <div class="progress-container">
            <div class="progress-header">
                <span>Прогресс до следующего уровня</span>
                <span id="progressText">0/7 дней</span>
            </div>
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill" style="width: 0%"></div>
            </div>
        </div>

        <button class="btn-primary" id="checkInBtn" onclick="checkIn()">
            ✅ Я справился сегодня
        </button>
        <button class="btn-secondary" onclick="resetHabit()" style="margin-top: 10px; background: rgba(239, 68, 68, 0.2); color: var(--danger); border-color: var(--danger);">
            🔄 Начать заново
        </button>
    </div>

    <!-- PvP Screen -->
    <div class="screen" id="pvpScreen">
        <div class="pvp-lobby" id="pvpLobby">
            <div class="lobby-header">
                <div class="lobby-title">⚔️ PvP Арена</div>
                <div class="lobby-subtitle">Соревнуйтесь с друзьями на выживание</div>
            </div>

            <div class="duel-options">
                <div class="duel-card" onclick="createDuel()">
                    <div class="duel-icon">🎲</div>
                    <div class="duel-info">
                        <div class="duel-name">Создать дуэль</div>
                        <div class="duel-desc">Сгенерировать код для друга</div>
                    </div>
                    <div class="duel-reward">+50 монет</div>
                </div>

                <div class="duel-card" onclick="showJoinInput()">
                    <div class="duel-icon">⚔️</div>
                    <div class="duel-info">
                        <div class="duel-name">Присоединиться</div>
                        <div class="duel-desc">Ввести код дуэли</div>
                    </div>
                    <div class="duel-reward">PvP</div>
                </div>
            </div>

            <div id="joinInput" style="display: none;">
                <div class="code-input-group">
                    <input type="text" class="code-input" id="joinCode" placeholder="XXXX" maxlength="4">
                    <button class="btn-primary" onclick="joinDuel()" style="width: auto; padding: 16px 24px;">Войти</button>
                </div>
            </div>

            <div class="share-code" id="shareCode" style="display: none;">
                <div style="font-size: 14px; color: var(--text-muted); margin-bottom: 8px;">Код дуэли:</div>
                <div class="code-display" id="duelCode">A7B2</div>
                <button class="copy-btn" onclick="copyCode()">📋 Копировать</button>
                <div style="margin-top: 12px; font-size: 12px; color: var(--text-muted);">
                    Отправь код другу. Кто дольше продержится — победитель!
                </div>
            </div>
        </div>

        <!-- PvP Arena Battle -->
        <div class="pvp-arena" id="pvpArena">
            <div class="battle-header">
                <div class="battle-title">🔥 Дуэль идет!</div>
                <div class="battle-timer" id="battleTimer">07:00:00</div>
                <div style="font-size: 12px; color: var(--text-muted); margin-top: 4px;">До финиша</div>
            </div>

            <div class="vs-divider">
                <div class="vs-line"></div>
                <div class="vs-text">VS</div>
                <div class="vs-line right"></div>
            </div>

            <div class="battle-field">
                <div class="player-side me" id="playerSide">
                    <div class="player-avatar">🌳</div>
                    <div class="player-name">Вы</div>
                    <div class="player-streak" id="myBattleStreak">12</div>
                    <div class="health-bar">
                        <div class="health-fill" id="myHealth" style="width: 80%"></div>
                    </div>
                    <div style="font-size: 12px; color: var(--text-muted);">дней без срыва</div>
                </div>

                <div class="player-side enemy" id="enemySide">
                    <div class="player-avatar">🥀</div>
                    <div class="player-name" id="enemyName">Противник</div>
                    <div class="player-streak" id="enemyBattleStreak">8</div>
                    <div class="health-bar">
                        <div class="health-fill" id="enemyHealth" style="width: 60%"></div>
                    </div>
                    <div style="font-size: 12px; color: var(--text-muted);" id="enemyStatus">онлайн</div>
                </div>
            </div>

            <div class="battle-actions">
                <button class="battle-btn btn-attack" onclick="tauntEnemy()">
                    😤 Трэш-ток
                </button>
                <button class="battle-btn btn-taunt" onclick="checkInBattle()">
                    ✅ Отметиться
                </button>
            </div>

            <div style="background: var(--surface); border-radius: 16px; padding: 16px; margin-bottom: 20px;">
                <div style="font-weight: 700; margin-bottom: 8px;">💰 Ставка: 50 монет</div>
                <div style="font-size: 13px; color: var(--text-muted);">
                    Победитель забирает все. При срыве — автоматический проигрыш.
                </div>
            </div>

            <button class="btn-secondary" onclick="surrender()" style="background: rgba(239, 68, 68, 0.2); color: var(--danger);">
                🏳️ Сдаться
            </button>
        </div>
    </div>

    <!-- Leaderboard Screen -->
    <div class="screen" id="leaderboardScreen">
        <div class="leaderboard">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                <div style="font-size: 20px; font-weight: 800;">🏆 Лидеры</div>
                <div style="font-size: 12px; color: var(--text-muted);">Топ-10 этого месяца</div>
            </div>

            <div id="leaderboardList">
                <div class="leader-item">
                    <div class="leader-rank gold">1</div>
                    <div class="leader-avatar">👑</div>
                    <div class="leader-info">
                        <div class="leader-name">Александр М.</div>
                        <div class="leader-score">45 дней • 12 побед</div>
                    </div>
                    <div class="leader-wins">1240💰</div>
                </div>

                <div class="leader-item">
                    <div class="leader-rank silver">2</div>
                    <div class="leader-avatar">🥈</div>
                    <div class="leader-info">
                        <div class="leader-name">Екатерина В.</div>
                        <div class="leader-score">38 дней • 8 побед</div>
                    </div>
                    <div class="leader-wins">890💰</div>
                </div>

                <div class="leader-item">
                    <div class="leader-rank bronze">3</div>
                    <div class="leader-avatar">🥉</div>
                    <div class="leader-info">
                        <div class="leader-name">Дмитрий К.</div>
                        <div class="leader-score">32 дня • 6 побед</div>
                    </div>
                    <div class="leader-wins">720💰</div>
                </div>

                <div class="leader-item" style="opacity: 0.6;">
                    <div class="leader-rank">4</div>
                    <div class="leader-avatar">🌟</div>
                    <div class="leader-info">
                        <div class="leader-name">Анна М.</div>
                        <div class="leader-score">28 дней • 4 победы</div>
                    </div>
                    <div class="leader-wins">540💰</div>
                </div>
            </div>

            <div style="margin-top: 20px; padding-top: 20px; border-top: 1px solid rgba(255,255,255,0.1); text-align: center; color: var(--text-muted); font-size: 13px;">
                Ваше место: <strong>#42</strong> из 1,247 игроков
            </div>
        </div>
    </div>
</div>

<!-- Taunt Bubble -->
<div class="taunt-bubble" id="tauntBubble"></div>

<!-- Modal -->
<div class="modal" id="resultModal">
    <div class="modal-content">
        <div class="modal-icon" id="resultIcon">🏆</div>
        <h2 class="modal-title" id="resultTitle">Победа!</h2>
        <p class="modal-text" id="resultText">Вы выиграли 50 монет</p>
        <button class="btn-secondary" onclick="closeResult()">Забрать награду</button>
    </div>
</div>

<!-- Toast -->
<div class="toast" id="toast"></div>

<script>
    // State
    let state = {
        currentHabit: 'smoking',
        streak: 0,
        totalDays: 0,
        coins: 100,
        pvpWins: 0,
        lastCheckIn: null,
        currentDuel: null, // { code, opponent, bet, startTime, myScore, enemyScore }
        achievements: []
    };

    const taunts = [
        "Ты уже сдался? 😏",
        "Мое дерево выше твоего! 🌳",
        "Готов проиграть свои монеты? 💰",
        "Сегодня я точно не сорвусь! 💪",
        "Твоя серия слишком короткая... 📏",
        "Я вижу твои руки трясутся! 😈",
        "Проиграешь и заплачешь 😂",
        "Мотивация на максимуме! 🔥"
    ];

    // Initialize
    function init() {
        loadState();
        renderStars();
        updateUI();
        checkDailyReset();
        simulateEnemyActivity();
        
        // Habit selector
        document.querySelectorAll('.habit-chip').forEach(chip => {
            chip.addEventListener('click', () => {
                document.querySelectorAll('.habit-chip').forEach(c => c.classList.remove('active'));
                chip.classList.add('active');
                state.currentHabit = chip.dataset.habit;
                saveState();
                showToast(`Трекер: ${chip.textContent}`);
            });
        });

        // Check URL for duel code
        const urlParams = new URLSearchParams(window.location.search);
        const duelCode = urlParams.get('duel');
        if (duelCode) {
            document.getElementById('joinCode').value = duelCode.toUpperCase();
            switchTab('pvp');
            showJoinInput();
        }
    }

    function renderStars() {
        const container = document.getElementById('stars');
        for (let i = 0; i < 20; i++) {
            const star = document.createElement('div');
            star.className = 'star';
            star.style.left = Math.random() * 100 + '%';
            star.style.top = Math.random() * 100 + '%';
            star.style.animationDelay = Math.random() * 3 + 's';
            container.appendChild(star);
        }
    }

    // Tab Switching
    function switchTab(tab) {
        document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
        document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
        
        if (tab === 'solo') {
            document.getElementById('soloScreen').classList.add('active');
            document.querySelector('[onclick="switchTab(\'solo\')"]').classList.add('active');
        } else if (tab === 'pvp') {
            document.getElementById('pvpScreen').classList.add('active');
            document.getElementById('pvpTab').classList.add('active');
            if (state.currentDuel) {
                showArena();
            }
        } else if (tab === 'leaderboard') {
            document.getElementById('leaderboardScreen').classList.add('active');
            document.querySelector('[onclick="switchTab(\'leaderboard\')"]').classList.add('active');
        }
    }

    // Solo Functions
    function checkIn() {
        const today = new Date().toDateString();
        
        if (state.lastCheckIn === today) {
            showToast('Уже отмечено! Возвращайтесь завтра 🌟');
            return;
        }

        state.streak++;
        state.totalDays++;
        state.lastCheckIn = today;
        
        if (state.currentDuel) {
            state.currentDuel.myScore = state.streak;
            checkBattleStatus();
        }
        
        saveState();
        updateUI();
        createConfetti();
        showToast(`+1 день! ${state.streak} дней без срыва! 🎉`);
        
        const tree = document.getElementById('tree');
        tree.style.transform = 'scale(1.1)';
        setTimeout(() => tree.style.transform = 'scale(1)', 300);
    }

    function resetHabit() {
        if (confirm('Сбросить прогресс? Дерево вернется к уровню 1.')) {
            state.streak = 0;
            if (state.currentDuel) {
                endBattle(false, "Вы сдались!");
            }
            saveState();
            updateUI();
            showToast('Новое начало! 💪');
        }
    }

    // PvP Functions
    function createDuel() {
        const code = Math.random().toString(36).substring(2, 6).toUpperCase();
        state.currentDuel = {
            code: code,
            opponent: "Ожидание...",
            bet: 50,
            startTime: Date.now(),
            myScore: state.streak,
            enemyScore: 0,
            active: false
        };
        
        document.getElementById('duelCode').textContent = code;
        document.getElementById('shareCode').style.display = 'block';
        document.getElementById('joinInput').style.display = 'none';
        
        // Simulate enemy joining after 3 seconds for demo
        setTimeout(() => {
            state.currentDuel.opponent = "Александр М.";
            state.currentDuel.enemyScore = Math.floor(Math.random() * 15) + 5;
            state.currentDuel.active = true;
            showToast('🎉 Противник присоединился!');
            document.getElementById('pvpBadge').classList.add('active');
            setTimeout(() => showArena(), 1000);
        }, 3000);
        
        saveState();
    }

    function showJoinInput() {
        document.getElementById('joinInput').style.display = 'block';
        document.getElementById('shareCode').style.display = 'none';
    }

    function joinDuel() {
        const code = document.getElementById('joinCode').value.toUpperCase();
        if (code.length !== 4) {
            showToast('Введите 4-символьный код!');
            return;
        }
        
        state.currentDuel = {
            code: code,
            opponent: "Екатерина В.",
            bet: 50,
            startTime: Date.now(),
            myScore: state.streak,
            enemyScore: Math.floor(Math.random() * 20) + 10,
            active: true
        };
        
        saveState();
        document.getElementById('pvpBadge').classList.add('active');
        showArena();
        showToast('Вы вступили в дуэль! Удачи! ⚔️');
    }

    function copyCode() {
        const code = document.getElementById('duelCode').textContent;
        navigator.clipboard.writeText(`Присоединяйся к дуэли в Growth Garden! Код: ${code} https://growthgarden.app/?duel=${code}`);
        showToast('Ссылка скопирована! Отправь другу 📋');
    }

    function showArena() {
        document.getElementById('pvpLobby').style.display = 'none';
        document.getElementById('pvpArena').classList.add('active');
        updateBattleUI();
        startBattleTimer();
    }

    function updateBattleUI() {
        if (!state.currentDuel) return;
        
        document.getElementById('myBattleStreak').textContent = state.streak;
        document.getElementById('enemyBattleStreak').textContent = state.currentDuel.enemyScore;
        document.getElementById('enemyName').textContent = state.currentDuel.opponent;
        
        // Health bars based on streak comparison
        const total = state.streak + state.currentDuel.enemyScore;
        const myPercent = total === 0 ? 50 : (state.streak / total) * 100;
        const enemyPercent = total === 0 ? 50 : (state.currentDuel.enemyScore / total) * 100;
        
        document.getElementById('myHealth').style.width = Math.min(myPercent, 100) + '%';
        document.getElementById('enemyHealth').style.width = Math.min(enemyPercent, 100) + '%';
    }

    function startBattleTimer() {
        let timeLeft = 7 * 24 * 60 * 60; // 7 days in seconds
        
        const timer = setInterval(() => {
            if (!state.currentDuel) {
                clearInterval(timer);
                return;
            }
            
            timeLeft--;
            const days = Math.floor(timeLeft / (24 * 60 * 60));
            const hours = Math.floor((timeLeft % (24 * 60 * 60)) / 3600);
            const mins = Math.floor((timeLeft % 3600) / 60);
            const secs = timeLeft % 60;
            
            document.getElementById('battleTimer').textContent = 
                `${String(days).padStart(2, '0')}:${String(hours).padStart(2, '0')}:${String(mins).padStart(2, '0')}`;
            
            if (timeLeft <= 0) {
                clearInterval(timer);
                determineWinner();
            }
        }, 1000);
    }

    function checkInBattle() {
        checkIn();
        updateBattleUI();
        
        // Simulate enemy response
        setTimeout(() => {
            if (Math.random() > 0.3 && state.currentDuel) {
                state.currentDuel.enemyScore++;
                updateBattleUI();
                showToast(`Противник отметился! ${state.currentDuel.enemyScore} дней 😤`);
            }
        }, 2000);
    }

    function tauntEnemy() {
        const taunt = taunts[Math.floor(Math.random() * taunts.length)];
        const bubble = document.getElementById('tauntBubble');
        bubble.textContent = taunt;
        bubble.classList.add('show');
        
        setTimeout(() => bubble.classList.remove('show'), 3000);
        
        // Simulate enemy taunt back
        setTimeout(() => {
            const enemyTaunts = [
                "Молчи и тренируйся! 🤫",
                "Пустые слова... 🙄",
                "Уже боишься? 😏",
                "Я сильнее тебя! 💪"
            ];
            bubble.textContent = enemyTaunts[Math.floor(Math.random() * enemyTaunts.length)];
            bubble.classList.add('show');
            setTimeout(() => bubble.classList.remove('show'), 3000);
        }, 3500);
    }

    function checkBattleStatus() {
        if (!state.currentDuel) return;
        
        if (state.streak > state.currentDuel.enemyScore + 7) {
            endBattle(true, "Вы обогнали противника на неделю!");
        }
    }

    function determineWinner() {
        if (!state.currentDuel) return;
        
        const won = state.streak >= state.currentDuel.enemyScore;
        endBattle(won, won ? "Время вышло! Вы победили!" : "Время вышло! Победил противник.");
    }

    function surrender() {
        if (confirm('Сдаться и потерять 50 монет?')) {
            endBattle(false, "Вы сдались...");
        }
    }

    function endBattle(won, reason) {
        state.currentDuel = null;
        document.getElementById('pvpBadge').classList.remove('active');
        saveState();
        
        const modal = document.getElementById('resultModal');
        document.getElementById('resultIcon').textContent = won ? '🏆' : '😞';
        document.getElementById('resultTitle').textContent = won ? 'Победа!' : 'Поражение';
        document.getElementById('resultText').textContent = reason;
        
        if (won) {
            state.coins += 50;
            state.pvpWins++;
            createConfetti();
        } else {
            state.coins = Math.max(0, state.coins - 50);
        }
        
        saveState();
        updateUI();
        modal.classList.add('active');
        
        setTimeout(() => {
            document.getElementById('pvpLobby').style.display = 'block';
            document.getElementById('pvpArena').classList.remove('active');
        }, 2000);
    }

    function closeResult() {
        document.getElementById('resultModal').classList.remove('active');
    }

    // Simulation
    function simulateEnemyActivity() {
        setInterval(() => {
            if (state.currentDuel && state.currentDuel.active && Math.random() > 0.7) {
                state.currentDuel.enemyScore++;
                updateBattleUI();
                
                if (document.getElementById('pvpArena').classList.contains('active')) {
                    showToast('Противник только что отметился! 🔥');
                }
            }
        }, 30000); // Every 30 seconds
    }

    // UI Updates
    function updateUI() {
        document.getElementById('currentStreak').textContent = state.streak;
        document.getElementById('totalDays').textContent = state.totalDays;
        document.getElementById('pvpWins').textContent = state.pvpWins;
        
        // Tree stage
        const tree = document.getElementById('tree');
        tree.className = 'tree';
        if (state.streak >= 100) tree.classList.add('stage-5');
        else if (state.streak >= 30) tree.classList.add('stage-4');
        else if (state.streak >= 7) tree.classList.add('stage-3');
        else if (state.streak >= 3) tree.classList.add('stage-2');
        else tree.classList.add('stage-1');
        
        // Progress
        const next = state.streak < 3 ? 3 : state.streak < 7 ? 7 : state.streak < 30 ? 30 : state.streak < 100 ? 100 : 365;
        const prev = state.streak < 3 ? 0 : state.streak < 7 ? 3 : state.streak < 30 ? 7 : state.streak < 100 ? 30 : 100;
        const progress = ((state.streak - prev) / (next - prev)) * 100;
        
        document.getElementById('progressFill').style.width = Math.max(progress, 5) + '%';
        document.getElementById('progressText').textContent = `${state.streak}/${next} дней`;
        
        // Button
        const today = new Date().toDateString();
        const btn = document.getElementById('checkInBtn');
        if (state.lastCheckIn === today) {
            btn.disabled = true;
            btn.innerHTML = '✅ Уже отмечено';
        } else {
            btn.disabled = false;
            btn.innerHTML = '✅ Я справился сегодня';
        }
    }

    function checkDailyReset() {
        const today = new Date().toDateString();
        if (state.lastCheckIn && state.lastCheckIn !== today) {
            const last = new Date(state.lastCheckIn);
            const diff = Math.floor((new Date() - last) / (1000 * 60 * 60 * 24));
            if (diff > 1) {
                if (state.currentDuel) {
                    endBattle(false, "Серия прервана! Вы пропустили день.");
                } else {
                    showToast(`Серия прервана после ${state.streak} дней 😔`);
                    state.streak = 0;
                    saveState();
                    updateUI();
                }
            }
        }
    }

    function createConfetti() {
        const colors = ['#10b981', '#34d399', '#f59e0b', '#f43f5e', '#60a5fa'];
        for (let i = 0; i < 30; i++) {
            const confetti = document.createElement('div');
            confetti.className = 'confetti';
            confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
            confetti.style.left = Math.random() * 100 + 'vw';
            confetti.style.top = '-10px';
            confetti.style.borderRadius = Math.random() > 0.5 ? '50%' : '0';
            document.body.appendChild(confetti);
            
            const anim = confetti.animate([
                { transform: `translateY(0) rotate(0deg)`, opacity: 1 },
                { transform: `translateY(${window.innerHeight}px) rotate(${Math.random() * 720}deg)`, opacity: 0 }
            ], { duration: 2000 + Math.random() * 2000 });
            
            anim.onfinish = () => confetti.remove();
        }
    }

    function showToast(msg) {
        const toast = document.getElementById('toast');
        toast.textContent = msg;
        toast.classList.add('show');
        setTimeout(() => toast.classList.remove('show'), 3000);
    }

    // Storage
    function saveState() {
        localStorage.setItem('growthGarden', JSON.stringify(state));
    }

    function loadState() {
        const saved = localStorage.getItem('growthGarden');
        if (saved) state = { ...state, ...JSON.parse(saved) };
    }

    init();
</script>

</body>
</html>
