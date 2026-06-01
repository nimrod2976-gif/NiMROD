<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NiMROD - محمل الوسائط الذكي</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800;900&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        :root {
            --bg-deep: #0a0a1a;
            --bg-card: rgba(15, 15, 35, 0.6);
            --glass: rgba(255, 255, 255, 0.05);
            --glass-border: rgba(255, 255, 255, 0.1);
            --text-primary: #e8e8f0;
            --text-secondary: #8a8ab0;
            --accent-blue: #00d4ff;
            --accent-purple: #7b2ff7;
            --accent-cyan: #00f5d4;
            --glow-blue: 0 0 20px rgba(0, 212, 255, 0.4), 0 0 40px rgba(0, 212, 255, 0.1);
            --glow-purple: 0 0 20px rgba(123, 47, 247, 0.4), 0 0 40px rgba(123, 47, 247, 0.1);
            --glow-cyan: 0 0 20px rgba(0, 245, 212, 0.4), 0 0 40px rgba(0, 245, 212, 0.1);
            --transition-smooth: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Tajawal', sans-serif;
            background: var(--bg-deep);
            color: var(--text-primary);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        /* Animated Background */
        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: 
                radial-gradient(ellipse at 20% 50%, rgba(0, 212, 255, 0.08) 0%, transparent 50%),
                radial-gradient(ellipse at 80% 20%, rgba(123, 47, 247, 0.08) 0%, transparent 50%),
                radial-gradient(ellipse at 50% 80%, rgba(0, 245, 212, 0.05) 0%, transparent 50%);
        }

        .bg-animation::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: 
                repeating-linear-gradient(
                    transparent,
                    transparent 50px,
                    rgba(0, 212, 255, 0.02) 50px,
                    rgba(0, 212, 255, 0.02) 51px
                );
            animation: bgMove 20s linear infinite;
        }

        @keyframes bgMove {
            0% { transform: translate(0, 0); }
            100% { transform: translate(50px, 50px); }
        }

        /* Floating Orbs */
        .orb {
            position: fixed;
            border-radius: 50%;
            filter: blur(80px);
            opacity: 0.3;
            z-index: -1;
            animation: float 8s ease-in-out infinite;
        }

        .orb-1 {
            width: 400px;
            height: 400px;
            background: var(--accent-blue);
            top: -100px;
            right: -100px;
            animation-delay: 0s;
        }

        .orb-2 {
            width: 300px;
            height: 300px;
            background: var(--accent-purple);
            bottom: -50px;
            left: -50px;
            animation-delay: -2s;
        }

        .orb-3 {
            width: 250px;
            height: 250px;
            background: var(--accent-cyan);
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation-delay: -4s;
        }

        @keyframes float {
            0%, 100% { transform: translate(0, 0) scale(1); }
            33% { transform: translate(30px, -30px) scale(1.1); }
            66% { transform: translate(-20px, 20px) scale(0.9); }
        }

        /* Header */
        header {
            padding: 2rem 1rem;
            text-align: center;
            position: relative;
        }

        .logo-container {
            display: inline-flex;
            align-items: center;
            gap: 1rem;
            position: relative;
        }

        .logo-n {
            font-family: 'Orbitron', sans-serif;
            font-size: 4rem;
            font-weight: 900;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple), var(--accent-cyan));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            position: relative;
            text-shadow: none;
            animation: logoGlow 3s ease-in-out infinite alternate;
        }

        @keyframes logoGlow {
            0% { filter: drop-shadow(0 0 10px rgba(0, 212, 255, 0.5)); }
            100% { filter: drop-shadow(0 0 30px rgba(123, 47, 247, 0.8)) drop-shadow(0 0 60px rgba(0, 245, 212, 0.3)); }
        }

        .logo-text {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.5rem;
            font-weight: 700;
            letter-spacing: 4px;
            color: var(--text-primary);
        }

        .logo-subtitle {
            font-size: 0.9rem;
            color: var(--text-secondary);
            margin-top: 0.5rem;
            letter-spacing: 2px;
        }

        /* Main Container */
        .main-container {
            max-width: 800px;
            margin: 0 auto;
            padding: 2rem 1rem;
        }

        /* Smart Downloader Box */
        .downloader-box {
            background: var(--glass);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border);
            border-radius: 24px;
            padding: 2.5rem;
            position: relative;
            overflow: hidden;
            transition: var(--transition-smooth);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
        }

        .downloader-box::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            border-radius: 24px;
            padding: 2px;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple), var(--accent-cyan), var(--accent-blue));
            background-size: 300% 300%;
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            opacity: 0.3;
            animation: borderGlow 4s ease infinite;
            transition: var(--transition-smooth);
        }

        @keyframes borderGlow {
            0%, 100% { background-position: 0% 50%; opacity: 0.3; }
            50% { background-position: 100% 50%; opacity: 0.6; }
        }

        .downloader-box.instagram::before {
            background: linear-gradient(135deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
            background-size: 300% 300%;
        }

        .downloader-box.tiktok::before {
            background: linear-gradient(135deg, #ff0050, #00f2ea, #000000, #ff0050);
            background-size: 300% 300%;
        }

        .downloader-box.facebook::before {
            background: linear-gradient(135deg, #1877f2, #42b72a, #1877f2);
            background-size: 300% 300%;
        }

        .downloader-box.youtube::before {
            background: linear-gradient(135deg, #ff0000, #ff4444, #cc0000);
            background-size: 300% 300%;
        }

        .downloader-box.x::before {
            background: linear-gradient(135deg, #000000, #1d9bf0, #000000);
            background-size: 300% 300%;
        }

        .downloader-box.active-platform::before {
            opacity: 0.8;
            animation: borderGlow 2s ease infinite;
        }

        .box-header {
            text-align: center;
            margin-bottom: 2rem;
            position: relative;
            z-index: 1;
        }

        .box-title {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 0.5rem;
        }

        .box-subtitle {
            color: var(--text-secondary);
            font-size: 0.9rem;
        }

        /* Platform Icons */
        .platform-icons {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            margin-bottom: 2rem;
            position: relative;
            z-index: 1;
        }

        .platform-icon {
            width: 48px;
            height: 48px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: var(--transition-smooth);
            position: relative;
            overflow: hidden;
        }

        .platform-icon::after {
            content: '';
            position: absolute;
            inset: 0;
            opacity: 0;
            transition: var(--transition-smooth);
        }

        .platform-icon.active {
            transform: translateY(-5px) scale(1.1);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        .platform-icon.active::after {
            opacity: 1;
        }

        .platform-icon.instagram.active {
            background: linear-gradient(135deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
            box-shadow: 0 0 20px rgba(220, 39, 67, 0.5);
        }

        .platform-icon.tiktok.active {
            background: linear-gradient(135deg, #ff0050, #00f2ea);
            box-shadow: 0 0 20px rgba(255, 0, 80, 0.5);
        }

        .platform-icon.facebook.active {
            background: #1877f2;
            box-shadow: 0 0 20px rgba(24, 119, 242, 0.5);
        }

        .platform-icon.youtube.active {
            background: #ff0000;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
        }

        .platform-icon.x.active {
            background: #000000;
            border-color: #1d9bf0;
            box-shadow: 0 0 20px rgba(29, 155, 240, 0.5);
        }

        /* URL Input */
        .input-group {
            position: relative;
            margin-bottom: 1.5rem;
            z-index: 1;
        }

        .url-input {
            width: 100%;
            padding: 1.2rem 1.5rem;
            padding-left: 3.5rem;
            background: rgba(0, 0, 0, 0.3);
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            color: var(--text-primary);
            font-family: 'Tajawal', sans-serif;
            font-size: 1rem;
            transition: var(--transition-smooth);
            outline: none;
        }

        .url-input:focus {
            border-color: var(--accent-blue);
            box-shadow: 0 0 20px rgba(0, 212, 255, 0.2);
        }

        .url-input.instagram:focus {
            border-color: #dc2743;
            box-shadow: 0 0 20px rgba(220, 39, 67, 0.3);
        }

        .url-input.tiktok:focus {
            border-color: #ff0050;
            box-shadow: 0 0 20px rgba(255, 0, 80, 0.3);
        }

        .url-input.facebook:focus {
            border-color: #1877f2;
            box-shadow: 0 0 20px rgba(24, 119, 242, 0.3);
        }

        .url-input.youtube:focus {
            border-color: #ff0000;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.3);
        }

        .url-input.x:focus {
            border-color: #1d9bf0;
            box-shadow: 0 0 20px rgba(29, 155, 240, 0.3);
        }

        .input-icon {
            position: absolute;
            left: 1.2rem;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-secondary);
            font-size: 1.2rem;
            transition: var(--transition-smooth);
        }

        .url-input:focus + .input-icon {
            color: var(--accent-blue);
        }

        /* Analyze Button */
        .analyze-btn {
            width: 100%;
            padding: 1.2rem;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            border: none;
            border-radius: 16px;
            color: white;
            font-family: 'Tajawal', sans-serif;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: var(--transition-smooth);
            z-index: 1;
        }

        .analyze-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            transition: 0.5s;
        }

        .analyze-btn:hover::before {
            left: 100%;
        }

        .analyze-btn:hover {
            transform: translateY(-2px);
            box-shadow: var(--glow-blue);
        }

        .analyze-btn:active {
            transform: translateY(0);
        }

        /* Results Section */
        .results-section {
            margin-top: 2rem;
            display: none;
            position: relative;
            z-index: 1;
        }

        .results-section.show {
            display: block;
            animation: fadeInUp 0.5s ease;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .preview-card {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 16px;
            overflow: hidden;
            margin-bottom: 1.5rem;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .preview-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.1), rgba(123, 47, 247, 0.1));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            color: var(--text-secondary);
        }

        .preview-info {
            padding: 1.5rem;
        }

        .preview-title {
            font-size: 1.1rem;
            font-weight: 700;
            margin-bottom: 0.5rem;
        }

        .preview-meta {
            color: var(--text-secondary);
            font-size: 0.85rem;
        }

        /* Quality Options */
        .quality-section {
            margin-bottom: 1.5rem;
        }

        .section-label {
            font-size: 0.9rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: var(--text-secondary);
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .quality-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 0.75rem;
        }

        .quality-option {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            padding: 1rem;
            cursor: pointer;
            transition: var(--transition-smooth);
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .quality-option:hover {
            background: rgba(255, 255, 255, 0.1);
            transform: translateY(-2px);
        }

        .quality-option.selected {
            border-color: var(--accent-blue);
            background: rgba(0, 212, 255, 0.1);
            box-shadow: 0 0 15px rgba(0, 212, 255, 0.2);
        }

        .quality-badge {
            font-size: 0.75rem;
            padding: 0.25rem 0.5rem;
            border-radius: 6px;
            background: rgba(0, 212, 255, 0.2);
            color: var(--accent-blue);
            font-weight: 600;
            margin-bottom: 0.5rem;
            display: inline-block;
        }

        .quality-size {
            font-size: 0.8rem;
            color: var(--text-secondary);
        }

        .quality-format {
            font-size: 0.7rem;
            color: var(--text-secondary);
            margin-top: 0.25rem;
        }

        /* Download Button */
        .download-btn {
            width: 100%;
            padding: 1rem;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-blue));
            border: none;
            border-radius: 12px;
            color: white;
            font-family: 'Tajawal', sans-serif;
            font-size: 1rem;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition-smooth);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }

        .download-btn:hover {
            transform: translateY(-2px);
            box-shadow: var(--glow-cyan);
        }

        /* Loading Animation */
        .loading-overlay {
            position: absolute;
            inset: 0;
            background: rgba(10, 10, 26, 0.9);
            backdrop-filter: blur(10px);
            display: none;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            gap: 1rem;
            z-index: 10;
            border-radius: 24px;
        }

        .loading-overlay.show {
            display: flex;
        }

        .loader {
            width: 60px;
            height: 60px;
            position: relative;
        }

        .loader-ring {
            position: absolute;
            inset: 0;
            border-radius: 50%;
            border: 3px solid transparent;
            border-top-color: var(--accent-blue);
            animation: spin 1s linear infinite;
        }

        .loader-ring:nth-child(2) {
            inset: 8px;
            border-top-color: var(--accent-purple);
            animation-duration: 1.5s;
            animation-direction: reverse;
        }

        .loader-ring:nth-child(3) {
            inset: 16px;
            border-top-color: var(--accent-cyan);
            animation-duration: 2s;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .loading-text {
            color: var(--text-secondary);
            font-size: 0.9rem;
        }

        /* Features Section */
        .features-section {
            margin-top: 3rem;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.5rem;
        }

        .feature-card {
            background: var(--glass);
            backdrop-filter: blur(10px);
            border: 1px solid var(--glass-border);
            border-radius: 16px;
            padding: 1.5rem;
            text-align: center;
            transition: var(--transition-smooth);
        }

        .feature-card:hover {
            transform: translateY(-5px);
            border-color: rgba(0, 212, 255, 0.3);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        .feature-icon {
            font-size: 2rem;
            margin-bottom: 1rem;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .feature-title {
            font-size: 1rem;
            font-weight: 700;
            margin-bottom: 0.5rem;
        }

        .feature-desc {
            font-size: 0.85rem;
            color: var(--text-secondary);
        }

        /* Footer */
        footer {
            margin-top: 4rem;
            padding: 2rem 1rem;
            text-align: center;
            position: relative;
        }

        .footer-content {
            max-width: 600px;
            margin: 0 auto;
        }

        .instagram-link {
            display: inline-flex;
            align-items: center;
            gap: 0.75rem;
            padding: 1rem 2rem;
            background: linear-gradient(135deg, rgba(240, 148, 51, 0.1), rgba(188, 24, 136, 0.1));
            border: 1px solid rgba(220, 39, 67, 0.3);
            border-radius: 50px;
            color: var(--text-primary);
            text-decoration: none;
            font-weight: 600;
            transition: var(--transition-smooth);
            position: relative;
            overflow: hidden;
        }

        .instagram-link::before {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(135deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
            opacity: 0;
            transition: var(--transition-smooth);
            z-index: -1;
        }

        .instagram-link:hover::before {
            opacity: 0.15;
        }

        .instagram-link:hover {
            transform: translateY(-3px);
            box-shadow: 0 0 30px rgba(220, 39, 67, 0.4), 0 0 60px rgba(188, 24, 136, 0.2);
            border-color: rgba(220, 39, 67, 0.6);
        }

        .instagram-link i {
            font-size: 1.5rem;
            background: linear-gradient(135deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .footer-text {
            margin-top: 1.5rem;
            color: var(--text-secondary);
            font-size: 0.85rem;
        }

        .footer-brand {
            font-family: 'Orbitron', sans-serif;
            font-weight: 700;
            color: var(--accent-blue);
        }

        /* Responsive */
        @media (max-width: 640px) {
            .logo-n {
                font-size: 3rem;
            }

            .logo-text {
                font-size: 1.2rem;
            }

            .downloader-box {
                padding: 1.5rem;
            }

            .platform-icons {
                gap: 1rem;
            }

            .platform-icon {
                width: 40px;
                height: 40px;
                font-size: 1.2rem;
            }

            .quality-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .features-section {
                grid-template-columns: 1fr;
            }
        }

        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--bg-deep);
        }

        ::-webkit-scrollbar-thumb {
            background: linear-gradient(var(--accent-blue), var(--accent-purple));
            border-radius: 4px;
        }

        /* Selection */
        ::selection {
            background: rgba(0, 212, 255, 0.3);
            color: white;
        }
    </style>
<base target="_blank">
</head>
<body>
    <div class="bg-animation"></div>
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>
    <div class="orb orb-3"></div>

    <header>
        <div class="logo-container">
            <span class="logo-n">N</span>
            <div>
                <div class="logo-text">NiMROD</div>
                <div class="logo-subtitle">محمل الوسائط الذكي</div>
            </div>
        </div>
    </header>

    <main class="main-container">
        <div class="downloader-box" id="downloaderBox">
            <div class="loading-overlay" id="loadingOverlay">
                <div class="loader">
                    <div class="loader-ring"></div>
                    <div class="loader-ring"></div>
                    <div class="loader-ring"></div>
                </div>
                <div class="loading-text">جاري التحليل...</div>
            </div>

            <div class="box-header">
                <h2 class="box-title">الصق رابط الوسائط</h2>
                <p class="box-subtitle">يدعم إنستغرام، تيك توك، فيسبوك، يوتيوب، وإكس</p>
            </div>

            <div class="platform-icons">
                <div class="platform-icon instagram" data-platform="instagram" title="إنستغرام">
                    <i class="fab fa-instagram"></i>
                </div>
                <div class="platform-icon tiktok" data-platform="tiktok" title="تيك توك">
                    <i class="fab fa-tiktok"></i>
                </div>
                <div class="platform-icon facebook" data-platform="facebook" title="فيسبوك">
                    <i class="fab fa-facebook-f"></i>
                </div>
                <div class="platform-icon youtube" data-platform="youtube" title="يوتيوب">
                    <i class="fab fa-youtube"></i>
                </div>
                <div class="platform-icon x" data-platform="x" title="إكس (تويتر)">
                    <i class="fab fa-x-twitter"></i>
                </div>
            </div>

            <div class="input-group">
                <input 
                    type="url" 
                    class="url-input" 
                    id="urlInput" 
                    placeholder="https://..."
                    autocomplete="off"
                >
                <i class="fas fa-link input-icon" id="inputIcon"></i>
            </div>

            <button class="analyze-btn" id="analyzeBtn">
                <i class="fas fa-search"></i>
                تحليل الرابط
            </button>

            <div class="results-section" id="resultsSection">
                <div class="preview-card">
                    <div class="preview-image" id="previewImage">
                        <i class="fas fa-image"></i>
                    </div>
                    <div class="preview-info">
                        <div class="preview-title" id="previewTitle">عنوان المحتوى</div>
                        <div class="preview-meta" id="previewMeta">مدة: 00:00 • المنصة</div>
                    </div>
                </div>

                <div class="quality-section">
                    <div class="section-label">
                        <i class="fas fa-video"></i>
                        خيارات التحميل
                    </div>
                    <div class="quality-grid" id="qualityGrid">
                        <!-- Generated by JS -->
                    </div>
                </div>

                <button class="download-btn" id="downloadBtn">
                    <i class="fas fa-download"></i>
                    تحميل الآن
                </button>
            </div>
        </div>

        <div class="features-section">
            <div class="feature-card">
                <div class="feature-icon">
                    <i class="fas fa-bolt"></i>
                </div>
                <div class="feature-title">تحميل سريع</div>
                <div class="feature-desc">تحميل فوري بدون انتظار أو إعلانات مزعجة</div>
            </div>
            <div class="feature-card">
                <div class="feature-icon">
                    <i class="fas fa-shield-alt"></i>
                </div>
                <div class="feature-title">آمن وموثوق</div>
                <div class="feature-desc">لا يتم تخزين أي بيانات أو روابط على خوادمنا</div>
            </div>
            <div class="feature-card">
                <div class="feature-icon">
                    <i class="fas fa-mobile-alt"></i>
                </div>
                <div class="feature-title">متجاوب بالكامل</div>
                <div class="feature-desc">يعمل بسلاسة على جميع الأجهزة والشاشات</div>
            </div>
            <div class="feature-card">
                <div class="feature-icon">
                    <i class="fas fa-magic"></i>
                </div>
                <div class="feature-title">ذكي تلقائياً</div>
                <div class="feature-desc">يتعرف على المنصة ويقدم أفضل جودة تلقائياً</div>
            </div>
        </div>
    </main>

    <footer>
        <div class="footer-content">
            <a href="https://instagram.com/nimrod.505" target="_blank" class="instagram-link">
                <i class="fab fa-instagram"></i>
                <span>@nimrod.505</span>
            </a>
            <div class="footer-text">
                صُنع بإتقان بواسطة <span class="footer-brand">NiMROD</span> © 2026
            </div>
        </div>
    </footer>

    <script>
        // Platform detection patterns
        const platforms = {
            instagram: {
                patterns: [/instagram\.com/, /instagr\.am/],
                color: '#dc2743',
                icon: 'fab fa-instagram',
                name: 'إنستغرام'
            },
            tiktok: {
                patterns: [/tiktok\.com/, /vm\.tiktok\.com/],
                color: '#ff0050',
                icon: 'fab fa-tiktok',
                name: 'تيك توك'
            },
            facebook: {
                patterns: [/facebook\.com/, /fb\.watch/, /fb\.me/],
                color: '#1877f2',
                icon: 'fab fa-facebook-f',
                name: 'فيسبوك'
            },
            youtube: {
                patterns: [/youtube\.com/, /youtu\.be/],
                color: '#ff0000',
                icon: 'fab fa-youtube',
                name: 'يوتيوب'
            },
            x: {
                patterns: [/twitter\.com/, /x\.com/, /t\.co/],
                color: '#1d9bf0',
                icon: 'fab fa-x-twitter',
                name: 'إكس'
            }
        };

        const urlInput = document.getElementById('urlInput');
        const downloaderBox = document.getElementById('downloaderBox');
        const inputIcon = document.getElementById('inputIcon');
        const analyzeBtn = document.getElementById('analyzeBtn');
        const loadingOverlay = document.getElementById('loadingOverlay');
        const resultsSection = document.getElementById('resultsSection');
        const qualityGrid = document.getElementById('qualityGrid');
        const previewTitle = document.getElementById('previewTitle');
        const previewMeta = document.getElementById('previewMeta');
        const previewImage = document.getElementById('previewImage');
        const downloadBtn = document.getElementById('downloadBtn');

        let detectedPlatform = null;
        let selectedQuality = null;

        // Detect platform from URL
        function detectPlatform(url) {
            for (const [key, platform] of Object.entries(platforms)) {
                for (const pattern of platform.patterns) {
                    if (pattern.test(url)) {
                        return key;
                    }
                }
            }
            return null;
        }

        // Update UI based on detected platform
        function updateUI(platform) {
            // Reset all
            downloaderBox.className = 'downloader-box';
            urlInput.className = 'url-input';
            document.querySelectorAll('.platform-icon').forEach(icon => {
                icon.classList.remove('active');
            });

            if (platform) {
                detectedPlatform = platform;
                const p = platforms[platform];

                // Update box border glow
                downloaderBox.classList.add(platform, 'active-platform');
                urlInput.classList.add(platform);

                // Highlight platform icon
                document.querySelector(`.platform-icon[data-platform="${platform}"]`).classList.add('active');

                // Update input icon
                inputIcon.className = `${p.icon} input-icon`;
                inputIcon.style.color = p.color;
            } else {
                detectedPlatform = null;
                inputIcon.className = 'fas fa-link input-icon';
                inputIcon.style.color = '';
            }
        }

        // URL input handler
        urlInput.addEventListener('input', (e) => {
            const url = e.target.value;
            const platform = detectPlatform(url);
            updateUI(platform);
        });

        // Paste handler
        urlInput.addEventListener('paste', (e) => {
            setTimeout(() => {
                const url = urlInput.value;
                const platform = detectPlatform(url);
                updateUI(platform);
            }, 0);
        });

        // Generate quality options based on platform
        function generateQualityOptions(platform) {
            const options = {
                instagram: [
                    { quality: 'HD', size: '1080p', format: 'MP4', label: 'فيديو عالي الجودة' },
                    { quality: 'SD', size: '720p', format: 'MP4', label: 'فيديو عادي' },
                    { quality: 'Audio', size: '128kbps', format: 'MP3', label: 'صوت فقط' }
                ],
                tiktok: [
                    { quality: 'HD', size: '1080p', format: 'MP4', label: 'بدون علامة مائية' },
                    { quality: 'SD', size: '720p', format: 'MP4', label: 'بدون علامة مائية' },
                    { quality: 'Audio', size: '128kbps', format: 'MP3', label: 'صوت فقط' }
                ],
                facebook: [
                    { quality: 'HD', size: '1080p', format: 'MP4', label: 'فيديو عالي الجودة' },
                    { quality: 'SD', size: '720p', format: 'MP4', label: 'فيديو عادي' },
                    { quality: 'Audio', size: '128kbps', format: 'MP3', label: 'صوت فقط' }
                ],
                youtube: [
                    { quality: '4K', size: '2160p', format: 'MP4', label: 'فيديو فائق الجودة' },
                    { quality: 'FHD', size: '1080p', format: 'MP4', label: 'فيديو عالي الجودة' },
                    { quality: 'HD', size: '720p', format: 'MP4', label: 'فيديو عادي' },
                    { quality: 'SD', size: '480p', format: 'MP4', label: 'فيديو اقتصادي' },
                    { quality: 'Audio', size: '320kbps', format: 'MP3', label: 'صوت عالي الجودة' }
                ],
                x: [
                    { quality: 'HD', size: '1080p', format: 'MP4', label: 'فيديو عالي الجودة' },
                    { quality: 'SD', size: '720p', format: 'MP4', label: 'فيديو عادي' },
                    { quality: 'Audio', size: '128kbps', format: 'MP3', label: 'صوت فقط' }
                ]
            };

            return options[platform] || options.youtube;
        }

        // Analyze button handler
        analyzeBtn.addEventListener('click', async () => {
            const url = urlInput.value.trim();

            if (!url) {
                urlInput.style.animation = 'shake 0.5s';
                setTimeout(() => urlInput.style.animation = '', 500);
                return;
            }

            const platform = detectPlatform(url);
            if (!platform) {
                alert('الرجاء إدخال رابط من منصة مدعومة (إنستغرام، تيك توك، فيسبوك، يوتيوب، إكس)');
                return;
            }

            // Show loading
            loadingOverlay.classList.add('show');
            resultsSection.classList.remove('show');

            // Simulate analysis (replace with actual API call)
            await new Promise(resolve => setTimeout(resolve, 2000));

            // Generate mock results
            const qualities = generateQualityOptions(platform);
            const p = platforms[platform];

            previewTitle.textContent = `محتوى من ${p.name}`;
            previewMeta.textContent = `مدة: 02:34 • ${p.name}`;
            previewImage.innerHTML = `<i class="${p.icon}" style="font-size: 4rem; color: ${p.color};"></i>`;

            qualityGrid.innerHTML = qualities.map((q, i) => `
                <div class="quality-option ${i === 0 ? 'selected' : ''}" data-index="${i}">
                    <div class="quality-badge">${q.quality}</div>
                    <div style="font-weight: 600; margin-bottom: 0.25rem;">${q.label}</div>
                    <div class="quality-size">${q.size}</div>
                    <div class="quality-format">${q.format}</div>
                </div>
            `).join('');

            selectedQuality = 0;

            // Add click handlers to quality options
            document.querySelectorAll('.quality-option').forEach(opt => {
                opt.addEventListener('click', () => {
                    document.querySelectorAll('.quality-option').forEach(o => o.classList.remove('selected'));
                    opt.classList.add('selected');
                    selectedQuality = parseInt(opt.dataset.index);
                });
            });

            // Hide loading and show results
            loadingOverlay.classList.remove('show');
            resultsSection.classList.add('show');
        });

        // Download button handler
        downloadBtn.addEventListener('click', () => {
            if (selectedQuality === null) return;

            const platform = detectedPlatform || 'youtube';
            const qualities = generateQualityOptions(platform);
            const quality = qualities[selectedQuality];

            // Simulate download
            downloadBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> جاري التحميل...';

            setTimeout(() => {
                downloadBtn.innerHTML = '<i class="fas fa-check"></i> تم التحميل!';
                downloadBtn.style.background = 'linear-gradient(135deg, #42b72a, #2d8f1a)';

                setTimeout(() => {
                    downloadBtn.innerHTML = '<i class="fas fa-download"></i> تحميل الآن';
                    downloadBtn.style.background = '';
                }, 2000);
            }, 2000);
        });

        // Add shake animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes shake {
                0%, 100% { transform: translateX(0); }
                25% { transform: translateX(-10px); }
                75% { transform: translateX(10px); }
            }
        `;
        document.head.appendChild(style);

        // Enter key handler
        urlInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                analyzeBtn.click();
            }
        });
    </script>
</body>
</html>
