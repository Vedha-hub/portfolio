<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vedhavathi Chennupati - Portfolio</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #6366f1;
            --accent-pink: #ec4899;
            --accent-cyan: #06b6d4;
            --accent-amber: #f59e0b;
            --dark-bg: #0f172a;
            --darker-bg: #0a0e27;
            --card-bg: rgba(15, 23, 42, 0.8);
            --text-primary: #f1f5f9;
            --text-secondary: #cbd5e1;
            --border-color: rgba(99, 102, 241, 0.2);
        }

        html {
            scroll-behavior: smooth;
            overflow-x: hidden;
        }

        body {
            font-family: 'DM Sans', sans-serif;
            background: linear-gradient(135deg, var(--dark-bg) 0%, var(--darker-bg) 100%);
            color: var(--text-primary);
            overflow-x: hidden;
            position: relative;
        }

        /* Noise Texture */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                url('data:image/svg+xml,%3Csvg viewBox="0 0 400 400" xmlns="http://www.w3.org/2000/svg"%3E%3Cfilter id="noiseFilter"%3E%3CfeTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="4" result="noise"/%3E%3C/filter%3E%3Crect width="400" height="400" filter="url(%23noiseFilter)" opacity="0.03"/%3E%3C/svg%3E');
            pointer-events: none;
            z-index: 1;
        }

        /* Particle Canvas */
        canvas#particleCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 12px;
        }

        ::-webkit-scrollbar-track {
            background: var(--darker-bg);
        }

        ::-webkit-scrollbar-thumb {
            background: linear-gradient(180deg, var(--accent-cyan), var(--accent-pink));
            border-radius: 6px;
            border: 2px solid var(--darker-bg);
        }

        ::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(180deg, var(--accent-pink), var(--accent-cyan));
        }

        /* Custom Cursor */
        body {
            cursor: none;
        }

        .cursor {
            position: fixed;
            width: 8px;
            height: 8px;
            background: radial-gradient(circle, var(--accent-cyan), var(--accent-pink));
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            box-shadow: 0 0 20px var(--accent-cyan), 0 0 40px var(--accent-pink);
            transition: all 0.1s ease-out;
        }

        .cursor-ring {
            position: fixed;
            width: 40px;
            height: 40px;
            border: 2px solid var(--accent-cyan);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9998;
            box-shadow: 0 0 15px var(--accent-cyan);
            transition: all 0.2s ease-out;
        }

        /* Loading Screen */
        .loader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--dark-bg) 0%, var(--darker-bg) 100%);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 10000;
            animation: fadeOut 0.8s ease-out 2s forwards;
        }

        @keyframes fadeOut {
            from {
                opacity: 1;
                visibility: visible;
            }
            to {
                opacity: 0;
                visibility: hidden;
            }
        }

        .loader-content {
            text-align: center;
        }

        .loader-initials {
            font-family: 'Syne', sans-serif;
            font-size: 5rem;
            font-weight: 800;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-pink), var(--accent-amber));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 2rem;
            animation: scaleIn 0.6s ease-out;
        }

        @keyframes scaleIn {
            from {
                transform: scale(0.5);
                opacity: 0;
            }
            to {
                transform: scale(1);
                opacity: 1;
            }
        }

        .progress-bar-container {
            width: 300px;
            height: 4px;
            background: rgba(99, 102, 241, 0.2);
            border-radius: 2px;
            overflow: hidden;
            border: 1px solid var(--border-color);
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--accent-cyan), var(--accent-pink), var(--accent-amber));
            border-radius: 2px;
            animation: progress 2s ease-in-out forwards;
        }

        @keyframes progress {
            from {
                width: 0%;
            }
            to {
                width: 100%;
            }
        }

        /* Navbar */
        .navbar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: 80px;
            background: rgba(15, 23, 42, 0.7);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--border-color);
            z-index: 1000;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 4rem;
            animation: slideDown 0.6s ease-out 1.5s backwards;
        }

        @keyframes slideDown {
            from {
                transform: translateY(-100%);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        .logo {
            font-family: 'Syne', sans-serif;
            font-size: 1.8rem;
            font-weight: 800;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-pink));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .nav-links {
            display: flex;
            gap: 3rem;
            list-style: none;
        }

        .nav-links a {
            color: var(--text-secondary);
            text-decoration: none;
            font-weight: 500;
            font-size: 0.95rem;
            position: relative;
            transition: color 0.3s ease;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: linear-gradient(90deg, var(--accent-cyan), var(--accent-pink));
            transition: width 0.3s ease;
        }

        .nav-links a:hover {
            color: var(--text-primary);
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        /* Main Content */
        main {
            position: relative;
            z-index: 2;
        }

        section {
            padding: 6rem 4rem;
            min-height: 100vh;
            display: flex;
            align-items: center;
        }

        .container {
            width: 100%;
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Hero Section */
        .hero {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            align-items: center;
            min-height: calc(100vh - 80px);
            margin-top: 80px;
        }

        .hero-left {
            animation: fadeInLeft 0.8s ease-out;
        }

        @keyframes fadeInLeft {
            from {
                opacity: 0;
                transform: translateX(-50px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .availability-tag {
            display: inline-block;
            background: rgba(6, 182, 212, 0.1);
            border: 1px solid var(--accent-cyan);
            color: var(--accent-cyan);
            padding: 0.5rem 1rem;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
        }

        .hero h1 {
            font-family: 'Syne', sans-serif;
            font-size: 4rem;
            font-weight: 800;
            line-height: 1.2;
            margin-bottom: 1.5rem;
            background: linear-gradient(135deg, #06b6d4 0%, #ec4899 50%, #f59e0b 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: shimmer 3s ease-in-out infinite;
            background-size: 200% 100%;
        }

        @keyframes shimmer {
            0%, 100% {
                background-position: 200% 0;
            }
            50% {
                background-position: -200% 0;
            }
        }

        .hero-subtitle {
            font-size: 1.5rem;
            color: var(--text-secondary);
            margin-bottom: 2rem;
            font-weight: 500;
        }

        .cta-buttons {
            display: flex;
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .btn {
            padding: 0.9rem 2rem;
            border: none;
            border-radius: 8px;
            font-family: 'Syne', sans-serif;
            font-weight: 600;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-pink));
            color: white;
            box-shadow: 0 10px 30px rgba(6, 182, 212, 0.3);
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(6, 182, 212, 0.4);
        }

        .btn-secondary {
            background: transparent;
            color: var(--text-primary);
            border: 2px solid var(--accent-pink);
            box-shadow: 0 10px 30px rgba(236, 72, 153, 0.2);
        }

        .btn-secondary:hover {
            transform: translateY(-3px);
            background: rgba(236, 72, 153, 0.1);
            box-shadow: 0 15px 40px rgba(236, 72, 153, 0.3);
        }

        .hero-right {
            animation: fadeInRight 0.8s ease-out;
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 500px;
        }

        @keyframes fadeInRight {
            from {
                opacity: 0;
                transform: translateX(50px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .floating-card {
            position: relative;
            width: 320px;
            height: 380px;
            background: rgba(15, 23, 42, 0.5);
            border: 1px solid var(--border-color);
            border-radius: 20px;
            padding: 2rem;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            animation: float 3s ease-in-out infinite;
            z-index: 5;
        }

        @keyframes float {
            0%, 100% {
                transform: translateY(0px) rotateZ(0deg);
            }
            50% {
                transform: translateY(-30px) rotateZ(2deg);
            }
        }

        .glowing-orb {
            position: absolute;
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, rgba(6, 182, 212, 0.3), transparent);
            border-radius: 50%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation: pulse 4s ease-in-out infinite;
            z-index: 1;
        }

        @keyframes pulse {
            0%, 100% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 0.3;
            }
            50% {
                transform: translate(-50%, -50%) scale(1.1);
                opacity: 0.5;
            }
        }

        .dashed-ring {
            position: absolute;
            width: 360px;
            height: 360px;
            border: 2px dashed var(--accent-pink);
            border-radius: 50%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation: spin 20s linear infinite;
            z-index: 2;
        }

        @keyframes spin {
            from {
                transform: translate(-50%, -50%) rotate(0deg);
            }
            to {
                transform: translate(-50%, -50%) rotate(360deg);
            }
        }

        .card-initials {
            font-family: 'Syne', sans-serif;
            font-size: 3rem;
            font-weight: 800;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-pink));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            z-index: 3;
        }

        .card-role {
            color: var(--text-secondary);
            font-size: 1rem;
            margin-top: 1rem;
            z-index: 3;
        }

        .card-stats {
            display: flex;
            justify-content: space-around;
            width: 100%;
            margin-top: 2rem;
            padding-top: 2rem;
            border-top: 1px solid var(--border-color);
            z-index: 3;
        }

        .stat {
            text-align: center;
        }

        .stat-number {
            font-family: 'Syne', sans-serif;
            font-size: 1.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-amber));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .stat-label {
            font-size: 0.75rem;
            color: var(--text-secondary);
            margin-top: 0.5rem;
        }

        /* Skills Section */
        #skills {
            background: linear-gradient(135deg, rgba(15, 23, 42, 0.5), rgba(10, 14, 39, 0.5));
        }

        .section-title {
            font-family: 'Syne', sans-serif;
            font-size: 3rem;
            font-weight: 800;
            margin-bottom: 4rem;
            color: var(--text-primary);
            animation: fadeInUp 0.6s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .skills-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        .skill-item {
            animation: slideUp 0.6s ease-out backwards;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .skill-name {
            display: flex;
            justify-content: space-between;
            margin-bottom: 0.8rem;
        }

        .skill-name-text {
            font-weight: 600;
            color: var(--text-primary);
        }

        .skill-percentage {
            color: var(--accent-cyan);
            font-weight: 600;
        }

        .skill-bar {
            width: 100%;
            height: 8px;
            background: rgba(99, 102, 241, 0.1);
            border-radius: 4px;
            overflow: hidden;
            border: 1px solid var(--border-color);
        }

        .skill-bar-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--accent-cyan), var(--accent-pink));
            border-radius: 4px;
            width: 0%;
            animation: fillBar 0.8s ease-out forwards;
            position: relative;
        }

        @keyframes fillBar {
            to {
                width: 100%;
            }
        }

        .skill-bar-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
            animation: shimmerBar 1.5s ease-in-out 0.8s;
        }

        @keyframes shimmerBar {
            from {
                transform: translateX(-100%);
            }
            to {
                transform: translateX(100%);
            }
        }

        .tech-cloud {
            margin-top: 4rem;
        }

        .tech-cloud-title {
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 2rem;
            color: var(--text-primary);
        }

        .tech-chips {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .tech-chip {
            background: rgba(6, 182, 212, 0.1);
            border: 1px solid var(--accent-cyan);
            color: var(--accent-cyan);
            padding: 0.6rem 1.2rem;
            border-radius: 50px;
            font-size: 0.9rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            animation: floatIn 0.6s ease-out backwards;
        }

        @keyframes floatIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .tech-chip:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 30px rgba(6, 182, 212, 0.3);
            background: rgba(6, 182, 212, 0.2);
            border-color: var(--accent-pink);
            color: var(--accent-pink);
        }

        /* Experience Section */
        #experience {
            padding-top: 3rem;
        }

        .timeline {
            position: relative;
            padding: 2rem 0;
        }

        .timeline::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            bottom: 0;
            width: 3px;
            background: linear-gradient(180deg, var(--accent-cyan), var(--accent-pink), var(--accent-amber));
            border-radius: 2px;
        }

        .timeline-item {
            margin-left: 3rem;
            margin-bottom: 3rem;
            animation: slideRight 0.6s ease-out backwards;
        }

        @keyframes slideRight {
            from {
                opacity: 0;
                transform: translateX(-30px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .timeline-dot {
            position: absolute;
            left: -9px;
            top: 0;
            width: 15px;
            height: 15px;
            background: var(--darker-bg);
            border: 2px solid var(--accent-pink);
            border-radius: 50%;
        }

        .experience-card {
            background: rgba(15, 23, 42, 0.5);
            border: 1px solid var(--border-color);
            padding: 2rem;
            border-radius: 12px;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .experience-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 0;
            height: 100%;
            background: linear-gradient(90deg, var(--accent-cyan), var(--accent-pink), transparent);
            opacity: 0;
            transition: all 0.5s ease;
        }

        .experience-card:hover {
            transform: translateX(10px) translateY(-5px);
            box-shadow: 0 20px 40px rgba(99, 102, 241, 0.2);
            border-color: var(--accent-pink);
        }

        .experience-card:hover::before {
            width: 3px;
            opacity: 1;
        }

        .exp-header {
            display: flex;
            justify-content: space-between;
            align-items: start;
            margin-bottom: 1rem;
        }

        .exp-title {
            font-family: 'Syne', sans-serif;
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--text-primary);
        }

        .exp-dates {
            font-size: 0.85rem;
            color: var(--accent-cyan);
            background: rgba(6, 182, 212, 0.1);
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            border: 1px solid var(--accent-cyan);
        }

        .exp-company {
            color: var(--accent-pink);
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        .exp-description {
            color: var(--text-secondary);
            line-height: 1.6;
            margin-bottom: 1rem;
        }

        .exp-badges {
            display: flex;
            flex-wrap: wrap;
            gap: 0.8rem;
        }

        .exp-badge {
            background: rgba(236, 72, 153, 0.1);
            border: 1px solid var(--accent-pink);
            color: var(--accent-pink);
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        /* Projects Section */
        #projects {
            background: linear-gradient(135deg, rgba(15, 23, 42, 0.5), rgba(10, 14, 39, 0.5));
        }

        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 2rem;
        }

        .project-card {
            background: rgba(15, 23, 42, 0.6);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 2rem;
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
            animation: fadeIn 0.6s ease-out backwards;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .project-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--accent-cyan), var(--accent-pink), transparent);
            opacity: 0;
            animation: none;
            transition: all 0.5s ease;
        }

        .project-card:hover::before {
            animation: gradientSweep 0.8s ease;
        }

        @keyframes gradientSweep {
            from {
                transform: translateX(-100%);
                opacity: 1;
            }
            to {
                transform: translateX(100%);
                opacity: 0;
            }
        }

        .project-card:hover {
            transform: translateY(-15px);
            box-shadow: 0 25px 50px rgba(6, 182, 212, 0.2);
            border-color: var(--accent-pink);
        }

        .project-emoji {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

        .project-title {
            font-family: 'Syne', sans-serif;
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--text-primary);
            margin-bottom: 0.8rem;
        }

        .project-description {
            color: var(--text-secondary);
            line-height: 1.6;
            margin-bottom: 1.5rem;
            font-size: 0.95rem;
        }

        .project-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 0.6rem;
        }

        .project-tag {
            background: rgba(245, 158, 11, 0.1);
            border: 1px solid var(--accent-amber);
            color: var(--accent-amber);
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        /* Education Section */
        #education {
            padding-top: 3rem;
        }

        .education-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        .education-card {
            background: rgba(15, 23, 42, 0.5);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 2rem;
            transition: all 0.3s ease;
            animation: fadeInUp 0.6s ease-out backwards;
        }

        .education-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(99, 102, 241, 0.2);
            border-color: var(--accent-cyan);
        }

        .education-degree {
            font-family: 'Syne', sans-serif;
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--text-primary);
            margin-bottom: 0.5rem;
        }

        .education-school {
            color: var(--accent-pink);
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        .education-years {
            color: var(--text-secondary);
            font-size: 0.9rem;
            margin-bottom: 1rem;
        }

        .language-badges {
            display: flex;
            flex-wrap: wrap;
            gap: 0.8rem;
            margin-top: 2rem;
        }

        .language-badge {
            background: linear-gradient(135deg, rgba(6, 182, 212, 0.1), rgba(236, 72, 153, 0.1));
            border: 1px solid var(--accent-cyan);
            color: var(--accent-cyan);
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 500;
            animation: pulseGlow 2s ease-in-out infinite;
        }

        @keyframes pulseGlow {
            0%, 100% {
                box-shadow: 0 0 10px rgba(6, 182, 212, 0.3);
            }
            50% {
                box-shadow: 0 0 20px rgba(6, 182, 212, 0.5);
            }
        }

        /* Contact Section */
        #contact {
            background: linear-gradient(135deg, rgba(15, 23, 42, 0.5), rgba(10, 14, 39, 0.5));
            display: flex;
            align-items: center;
        }

        .contact-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
            width: 100%;
        }

        .contact-info {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .contact-card {
            background: rgba(15, 23, 42, 0.5);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 1.5rem;
            transition: all 0.3s ease;
            animation: slideLeft 0.6s ease-out backwards;
            position: relative;
            overflow: hidden;
        }

        @keyframes slideLeft {
            from {
                opacity: 0;
                transform: translateX(-50px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .contact-card:hover {
            transform: translateX(10px);
            box-shadow: 0 15px 35px rgba(236, 72, 153, 0.2);
            border-color: var(--accent-pink);
        }

        .contact-label {
            font-size: 0.85rem;
            color: var(--text-secondary);
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        .contact-value {
            font-size: 1.1rem;
            color: var(--text-primary);
            font-weight: 600;
            word-break: break-all;
        }

        .contact-avatar {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 2rem;
        }

        .avatar-initials {
            font-family: 'Syne', sans-serif;
            font-size: 4rem;
            font-weight: 800;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-pink));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            position: relative;
            animation: pulseInitials 2s ease-in-out infinite;
        }

        @keyframes pulseInitials {
            0%, 100% {
                transform: scale(1);
                filter: drop-shadow(0 0 10px rgba(6, 182, 212, 0.5));
            }
            50% {
                transform: scale(1.05);
                filter: drop-shadow(0 0 20px rgba(236, 72, 153, 0.5));
            }
        }

        .ripple-ring {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            border: 2px solid var(--accent-cyan);
            border-radius: 50%;
            opacity: 0;
        }

        .ripple-ring.ring-1 {
            width: 120px;
            height: 120px;
            animation: ripple 2s ease-out infinite;
        }

        .ripple-ring.ring-2 {
            width: 160px;
            height: 160px;
            animation: ripple 2s ease-out 0.5s infinite;
        }

        .ripple-ring.ring-3 {
            width: 200px;
            height: 200px;
            animation: ripple 2s ease-out 1s infinite;
        }

        @keyframes ripple {
            from {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1);
            }
            to {
                opacity: 0;
                transform: translate(-50%, -50%) scale(1.5);
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .navbar {
                padding: 0 2rem;
            }

            .logo {
                font-size: 1.3rem;
            }

            .nav-links {
                gap: 1.5rem;
            }

            .nav-links a {
                font-size: 0.85rem;
            }

            section {
                padding: 4rem 2rem;
            }

            .hero {
                grid-template-columns: 1fr;
                gap: 2rem;
                min-height: auto;
            }

            .hero-left {
                text-align: center;
            }

            .hero h1 {
                font-size: 2.5rem;
            }

            .hero-subtitle {
                font-size: 1.2rem;
            }

            .cta-buttons {
                flex-direction: column;
                align-items: center;
            }

            .hero-right {
                min-height: 400px;
            }

            .floating-card {
                width: 280px;
                height: 340px;
            }

            .section-title {
                font-size: 2rem;
                margin-bottom: 2rem;
            }

            .skills-grid {
                grid-template-columns: 1fr;
            }

            .projects-grid {
                grid-template-columns: 1fr;
            }

            .contact-grid {
                grid-template-columns: 1fr;
                gap: 2rem;
            }

            .contact-avatar {
                display: none;
            }

            .timeline::before {
                left: 0;
            }

            .timeline-item {
                margin-left: 2rem;
            }
        }
    </style>
</head>
<body>
    <!-- Canvas for particle animation -->
    <canvas id="particleCanvas"></canvas>

    <!-- Custom Cursor -->
    <div class="cursor"></div>
    <div class="cursor-ring"></div>

    <!-- Loading Screen -->
    <div class="loader">
        <div class="loader-content">
            <div class="loader-initials">VC</div>
            <div class="progress-bar-container">
                <div class="progress-bar"></div>
            </div>
        </div>
    </div>

    <!-- Navigation -->
    <nav class="navbar">
        <div class="logo">VC</div>
        <ul class="nav-links">
            <li><a href="#hero">Home</a></li>
            <li><a href="#skills">Skills</a></li>
            <li><a href="#experience">Experience</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#education">Education</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>

    <main>
        <!-- Hero Section -->
        <section id="hero" class="hero">
            <div class="hero-left">
                <div class="availability-tag">✨ Open to Internships</div>
                <h1>Vedhavathi Chennupati</h1>
                <p class="hero-subtitle">Software Developer & Data Enthusiast</p>
                <div class="cta-buttons">
                    <button class="btn btn-primary" onclick="document.getElementById('contact').scrollIntoView({behavior: 'smooth'})">Get in Touch</button>
                    <button class="btn btn-secondary" onclick="window.open('mailto:20240802300@dypiu.ac.in')">Send Email</button>
                </div>
            </div>

            <div class="hero-right">
                <div class="glowing-orb"></div>
                <div class="dashed-ring"></div>
                <div class="floating-card">
                    <div class="card-initials">VC</div>
                    <div class="card-role">CS Engineering Student</div>
                    <div class="card-stats">
                        <div class="stat">
                            <div class="stat-number">3+</div>
                            <div class="stat-label">Projects</div>
                        </div>
                        <div class="stat">
                            <div class="stat-number">8</div>
                            <div class="stat-label">Skills</div>
                        </div>
                        <div class="stat">
                            <div class="stat-number">3</div>
                            <div class="stat-label">Certifications</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Skills Section -->
        <section id="skills">
            <div class="container">
                <h2 class="section-title">Technical Skills</h2>
                <div class="skills-grid">
                    <div class="skill-item">
                        <div class="skill-name">
                            <span class="skill-name-text">Python</span>
                            <span class="skill-percentage">90%</span>
                        </div>
                        <div class="skill-bar">
                            <div class="skill-bar-fill" style="animation-delay: 0s"></div>
                        </div>
                    </div>

                    <div class="skill-item">
                        <div class="skill-name">
                            <span class="skill-name-text">Web Development (React & Next.js)</span>
                            <span class="skill-percentage">85%</span>
                        </div>
                        <div class="skill-bar">
                            <div class="skill-bar-fill" style="animation-delay: 0.1s; width: 85%"></div>
                        </div>
                    </div>

                    <div class="skill-item">
                        <div class="skill-name">
                            <span class="skill-name-text">C++</span>
                            <span class="skill-percentage">75%</span>
                        </div>
                        <div class="skill-bar">
                            <div class="skill-bar-fill" style="animation-delay: 0.2s; width: 75%"></div>
                        </div>
                    </div>

                    <div class="skill-item">
                        <div class="skill-name">
                            <span class="skill-name-text">Data Science & ML</span>
                            <span class="skill-percentage">80%</span>
                        </div>
                        <div class="skill-bar">
                            <div class="skill-bar-fill" style="animation-delay: 0.3s; width: 80%"></div>
                        </div>
                    </div>

                    <div class="skill-item">
                        <div class="skill-name">
                            <span class="skill-name-text">SQL & Databases</span>
                            <span class="skill-percentage">78%</span>
                        </div>
                        <div class="skill-bar">
                            <div class="skill-bar-fill" style="animation-delay: 0.4s; width: 78%"></div>
                        </div>
                    </div>

                    <div class="skill-item">
                        <div class="skill-name">
                            <span class="skill-name-text">Git & Version Control</span>
                            <span class="skill-percentage">82%</span>
                        </div>
                        <div class="skill-bar">
                            <div class="skill-bar-fill" style="animation-delay: 0.5s; width: 82%"></div>
                        </div>
                    </div>
                </div>

                <div class="tech-cloud">
                    <h3 class="tech-cloud-title">Technologies & Tools</h3>
                    <div class="tech-chips">
                        <div class="tech-chip">JavaScript</div>
                        <div class="tech-chip">HTML/CSS</div>
                        <div class="tech-chip">Tailwind CSS</div>
                        <div class="tech-chip">React</div>
                        <div class="tech-chip">Next.js</div>
                        <div class="tech-chip">OpenCV</div>
                        <div class="tech-chip">NumPy</div>
                        <div class="tech-chip">Pandas</div>
                        <div class="tech-chip">Matplotlib</div>
                        <div class="tech-chip">Git</div>
                        <div class="tech-chip">GitHub</div>
                        <div class="tech-chip">VS Code</div>
                        <div class="tech-chip">Vercel</div>
                        <div class="tech-chip">LaTeX</div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Experience Section -->
        <section id="experience">
            <div class="container">
                <h2 class="section-title">Leadership & Involvement</h2>
                <div class="timeline">
                    <div class="timeline-item">
                        <div class="timeline-dot"></div>
                        <div class="experience-card">
                            <div class="exp-header">
                                <div>
                                    <div class="exp-title">Design & Photography Lead</div>
                                    <div class="exp-company">Mindscape Club, DYPIU</div>
                                </div>
                                <div class="exp-dates">Aug 2024 - Present</div>
                            </div>
                            <p class="exp-description">Led visual identity design for university events, producing promotional posters and digital assets for major college festivals. Developed strong communication and creative skills through event coordination and mentorship.</p>
                            <div class="exp-badges">
                                <span class="exp-badge">Design</span>
                                <span class="exp-badge">Leadership</span>
                                <span class="exp-badge">Event Management</span>
                            </div>
                        </div>
                    </div>

                    <div class="timeline-item">
                        <div class="timeline-dot"></div>
                        <div class="experience-card">
                            <div class="exp-header">
                                <div>
                                    <div class="exp-title">University Mentor</div>
                                    <div class="exp-company">Induction Program, DYPIU</div>
                                </div>
                                <div class="exp-dates">2026</div>
                            </div>
                            <p class="exp-description">Mentored incoming students during the University Induction Program. Demonstrated strong communication and teamwork skills while guiding freshers through their academic journey.</p>
                            <div class="exp-badges">
                                <span class="exp-badge">Mentorship</span>
                                <span class="exp-badge">Communication</span>
                                <span class="exp-badge">Teamwork</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Projects Section -->
        <section id="projects">
            <div class="container">
                <h2 class="section-title">Featured Projects</h2>
                <div class="projects-grid">
                    <div class="project-card">
                        <div class="project-emoji">💼</div>
                        <h3 class="project-title">Personal Portfolio</h3>
                        <p class="project-description">High-performance responsive web portfolio with custom Canvas API animated background and CI/CD pipeline integration via Vercel for automated deployment.</p>
                        <div class="project-tags">
                            <span class="project-tag">Next.js</span>
                            <span class="project-tag">React</span>
                            <span class="project-tag">Tailwind CSS</span>
                            <span class="project-tag">Vercel</span>
                        </div>
                    </div>

                    <div class="project-card">
                        <div class="project-emoji">📦</div>
                        <h3 class="project-title">Smart Inventory System</h3>
                        <p class="project-description">DIP Toolkit featuring image manipulation and analysis tools using OpenCV to automate inventory stock-checking and streamline warehouse management.</p>
                        <div class="project-tags">
                            <span class="project-tag">Python</span>
                            <span class="project-tag">OpenCV</span>
                            <span class="project-tag">Image Processing</span>
                        </div>
                    </div>

                    <div class="project-card">
                        <div class="project-emoji">🎨</div>
                        <h3 class="project-title">Digital Design Assets</h3>
                        <p class="project-description">Comprehensive collection of promotional posters and digital assets created for major college festivals and events. Showcases creative design and branding capabilities.</p>
                        <div class="project-tags">
                            <span class="project-tag">Design</span>
                            <span class="project-tag">Branding</span>
                            <span class="project-tag">Visual Identity</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Education Section -->
        <section id="education">
            <div class="container">
                <h2 class="section-title">Education & Certifications</h2>
                <div class="education-grid">
                    <div class="education-card">
                        <div class="education-degree">B.Tech in CSE</div>
                        <div class="education-school">DY Patil International University</div>
                        <div class="education-years">2024 – Present | Pune, MH</div>
                        <p style="color: var(--text-secondary); line-height: 1.6;">Currently in 2nd year, pursuing Computer Science and Engineering with focus on software development and data analytics.</p>
                    </div>

                    <div class="education-card">
                        <div class="education-degree">Class XII (PCM)</div>
                        <div class="education-school">Sri Chaitanya Techno School</div>
                        <div class="education-years">2022 – 2024 | Pune, MH</div>
                        <p style="color: var(--text-secondary); line-height: 1.6;">Completed senior secondary education with Physics, Chemistry, and Mathematics specialization.</p>
                    </div>

                    <div class="education-card">
                        <div class="education-degree">Board of Secondary Education</div>
                        <div class="education-school">Pawar Public School</div>
                        <div class="education-years">2021 – 2022 | Pune, India</div>
                        <p style="color: var(--text-secondary); line-height: 1.6;">Completed secondary education with strong foundation in academics and extracurricular activities.</p>
                    </div>
                </div>

                <div class="language-badges" style="margin-top: 4rem;">
                    <h3 class="section-title" style="grid-column: 1/-1; margin-bottom: 2rem; font-size: 1.8rem;">Recent Certifications</h3>
                    <div class="language-badge">GenAI Data Analytics - Tata (Forage) - Apr 2026</div>
                    <div class="language-badge">Data Mining in Python - Coursera - Apr 2026</div>
                    <div class="language-badge">Technology Commercialization - U. Rochester - Feb 2026</div>
                </div>
            </div>
        </section>

        <!-- Contact Section -->
        <section id="contact">
            <div class="container">
                <div class="contact-grid">
                    <div class="contact-info">
                        <h2 class="section-title" style="margin-bottom: 2rem;">Get in Touch</h2>
                        <div class="contact-card">
                            <div class="contact-label">Email</div>
                            <div class="contact-value">20240802300@dypiu.ac.in</div>
                        </div>

                        <div class="contact-card">
                            <div class="contact-label">Phone</div>
                            <div class="contact-value">+91 8421191922</div>
                        </div>

                        <div class="contact-card">
                            <div class="contact-label">Location</div>
                            <div class="contact-value">Pune, Maharashtra, India</div>
                        </div>

                        <div class="contact-card">
                            <div class="contact-label">Availability</div>
                            <div class="contact-value">Open to Internship Opportunities</div>
                        </div>
                    </div>

                    <div class="contact-avatar">
                        <div class="avatar-initials">VC</div>
                        <div class="ripple-ring ring-1"></div>
                        <div class="ripple-ring ring-2"></div>
                        <div class="ripple-ring ring-3"></div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <script>
        // ==================== CUSTOM CURSOR ====================
        const cursor = document.querySelector('.cursor');
        const cursorRing = document.querySelector('.cursor-ring');

        let mouseX = 0;
        let mouseY = 0;

        document.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;

            cursor.style.left = mouseX + 'px';
            cursor.style.top = mouseY + 'px';

            setTimeout(() => {
                cursorRing.style.left = mouseX - 20 + 'px';
                cursorRing.style.top = mouseY - 20 + 'px';
            }, 100);
        });

        // ==================== PARTICLE ANIMATION ====================
        const canvas = document.getElementById('particleCanvas');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const particles = [];
        const particleCount = 50;
        const colors = ['#06b6d4', '#ec4899', '#f59e0b', '#6366f1'];

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.vx = (Math.random() - 0.5) * 2;
                this.vy = (Math.random() - 0.5) * 2;
                this.radius = Math.random() * 2 + 1;
                this.color = colors[Math.floor(Math.random() * colors.length)];
            }

            update() {
                this.x += this.vx;
                this.y += this.vy;

                if (this.x < 0) this.x = canvas.width;
                if (this.x > canvas.width) this.x = 0;
                if (this.y < 0) this.y = canvas.height;
                if (this.y > canvas.height) this.y = 0;
            }

            draw() {
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function initParticles() {
            for (let i = 0; i < particleCount; i++) {
                particles.push(new Particle());
            }
        }

        function drawConnections() {
            for (let i = 0; i < particles.length; i++) {
                for (let j = i + 1; j < particles.length; j++) {
                    const dx = particles[i].x - particles[j].x;
                    const dy = particles[i].y - particles[j].y;
                    const distance = Math.sqrt(dx * dx + dy * dy);

                    if (distance < 150) {
                        ctx.strokeStyle = `rgba(99, 102, 241, ${0.1 * (1 - distance / 150)})`;
                        ctx.lineWidth = 1;
                        ctx.beginPath();
                        ctx.moveTo(particles[i].x, particles[i].y);
                        ctx.lineTo(particles[j].x, particles[j].y);
                        ctx.stroke();
                    }
                }
            }
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            particles.forEach(particle => {
                particle.update();
                particle.draw();
            });

            drawConnections();
            requestAnimationFrame(animate);
        }

        initParticles();
        animate();

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        // ==================== SCROLL ANIMATIONS ====================
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.animation = getAnimation(entry.target);
                    entry.target.style.opacity = '1';
                }
            });
        }, observerOptions);

        function getAnimation(element) {
            const className = element.className;
            if (className.includes('skill-item')) {
                return 'slideUp 0.6s ease-out forwards';
            } else if (className.includes('timeline-item')) {
                return 'slideRight 0.6s ease-out forwards';
            } else if (className.includes('project-card')) {
                return 'fadeIn 0.6s ease-out forwards';
            } else if (className.includes('education-card')) {
                return 'fadeInUp 0.6s ease-out forwards';
            } else if (className.includes('contact-card')) {
                return 'slideLeft 0.6s ease-out forwards';
            }
            return 'fadeInUp 0.6s ease-out forwards';
        }

        // Observe elements
        document.querySelectorAll('.skill-item, .timeline-item, .project-card, .education-card, .contact-card, .tech-chip').forEach(el => {
            observer.observe(el);
            el.style.opacity = '0';
        });

        // ==================== SKILL BAR ANIMATION ====================
        const skillObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const skillBar = entry.target.querySelector('.skill-bar-fill');
                    if (skillBar) {
                        const width = skillBar.style.width || '100%';
                        skillBar.style.animation = `fillBar 0.8s ease-out forwards`;
                    }
                }
            });
        }, { threshold: 0.5 });

        document.querySelectorAll('.skill-item').forEach(item => {
            skillObserver.observe(item);
        });

        // ==================== SMOOTH SCROLL ====================
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                }
            });
        });

        // ==================== STAGGER ANIMATIONS ====================
        document.querySelectorAll('.skill-item').forEach((item, index) => {
            item.style.animationDelay = `${index * 0.1}s`;
        });

        document.querySelectorAll('.timeline-item').forEach((item, index) => {
            item.style.animationDelay = `${index * 0.2}s`;
        });

        document.querySelectorAll('.project-card').forEach((card, index) => {
            card.style.animationDelay = `${index * 0.15}s`;
        });

        document.querySelectorAll('.education-card').forEach((card, index) => {
            card.style.animationDelay = `${index * 0.15}s`;
        });

        document.querySelectorAll('.tech-chip').forEach((chip, index) => {
            chip.style.animationDelay = `${0.1 + index * 0.05}s`;
        });
    </script>
</body>
</html>
