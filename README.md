<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Heather Rosenau | CAD Specification Sheet</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400;700&family=Orbitron:wght@700&display=swap" rel="stylesheet">
    <style>
        /* =================================
           I. GLOBAL & THEME
           ================================= */
        :root {
            --color-bg: #0d273f; /* Deep Blueprint Blue */
            --color-card: #1f3d57; /* Dark Panel Blue */
            --color-accent: #00bcd4; /* Cyan/Aqua Accent */
            --color-text: #f0f0f0; /* Off-White Text */
            --font-main: 'Roboto Mono', monospace;
            --font-heading: 'Orbitron', sans-serif;
        }

        body {
            font-family: var(--font-main);
            background-color: var(--color-bg);
            color: var(--color-text);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 10px; /* Reduced padding for mobile */
            background-image:
                linear-gradient(to right, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
            background-size: 20px 20px;
        }

        /* =================================
           II. MAIN CARD LAYOUT (Mobile-First)
           ================================= */
        .drawing-sheet {
            position: relative;
            background: var(--color-card);
            border: 3px solid var(--color-accent);
            border-radius: 5px;
            box-shadow: 0 0 15px rgba(0, 188, 212, 0.3);
            max-width: 800px;
            width: 100%;
            padding: 15px; /* Reduced padding for mobile */
            display: flex; /* Using flex for simple stacking */
            flex-direction: column;
            gap: 15px;
        }
        
        /* Mobile: Content stacks vertically */
        .title-block, .content-area {
            order: 1; /* Default order */
        }
        .detail-panels-wrapper {
            order: 3; /* Always at the bottom */
            padding-top: 5px;
            border-top: 1px dashed rgba(255, 255, 255, 0.3);
        }
        .content-area {
            order: 2; /* Main description should come after title/contact */
        }

        /* Profile picture, H1, Job Title, and Spec Box styles */
        .title-block {
            text-align: center;
        }
        .title-block h1 {
            font-family: var(--font-heading);
            font-size: 2em; /* Slightly reduced for mobile */
            color: var(--color-accent);
            margin: 0 0 5px 0;
            line-height: 1.1;
            text-transform: uppercase;
        }
        .title-block .job-title {
            font-size: 0.9em;
            color: var(--color-text);
            margin-bottom: 15px;
        }
        .profile-pic {
            width: 100px; /* Smaller picture for mobile */
            height: 100px;
            border-radius: 50%;
            border: 4px solid var(--color-accent);
            box-shadow: 0 0 10px rgba(0, 188, 212, 0.5);
            margin-bottom: 15px;
            display: block;
            margin-left: auto;
            margin-right: auto;
        }
        /* Spec Box - Contact Info (Stacking on mobile) */
        .spec-box {
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 10px;
            background: rgba(0, 0, 0, 0.1);
            text-align: left;
            font-size: 0.85em; /* Smaller font for contact details */
            margin-top: 15px;
        }
        .spec-box p {
            margin: 5px 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap; /* Allows contact details to wrap if names are long */
        }
        .spec-box strong {
            color: var(--color-accent);
            margin-right: 10px;
            flex-basis: 30%; /* Gives label space */
        }
        .spec-box a {
            color: var(--color-text);
            text-decoration: none;
            flex-basis: 60%; /* Gives value space */
            text-align: right;
        }
        .spec-box a:hover {
            color: var(--color-accent);
        }

        /* =================================
           III. NAVIGATION AND BUTTONS
           ================================= */
        .content-area {
            padding: 0;
        }
        .content-area p {
            font-size: 0.9em;
        }
        .contact-actions {
            display: flex;
            flex-wrap: wrap; /* Buttons wrap on mobile */
            gap: 8px; /* Smaller gap on mobile */
            margin-bottom: 15px;
            justify-content: center;
        }
        .contact-actions a {
            padding: 8px 10px; /* Smaller buttons for mobile */
            background: var(--color-accent);
            color: var(--color-bg);
            text-decoration: none;
            border-radius: 3px;
            font-weight: 700;
            font-size: 0.8em; /* Smaller text */
            transition: background 0.3s, transform 0.2s;
            text-transform: uppercase;
            flex: 1 1 45%; /* Two buttons per row on mobile */
            text-align: center;
            max-width: 150px;
        }
        .contact-actions a:hover {
            background: #0097a7;
            transform: translateY(-1px);
        }

        /* Active state for navigation */
        .contact-actions a:focus,
        .contact-actions a:active {
            background: #9b59b6; 
            color: var(--color-text);
        }
        
        /* =================================
           IV. CSS-ONLY TOGGLE (The Sibling Trick)
           ================================= */
        .detail-panels-wrapper {
            /* This is the container for the elements that will be targeted */
            grid-column: 1 / 3;
            margin-top: 0;
            padding-top: 0;
            border-top: none; 
        }

        .hidden-section {
            /* Initial Hidden State */
            max-height: 0;
            overflow: hidden;
            opacity: 0;
            padding: 0 10px; 
            margin-bottom: 0;
            transition: max-height 0.5s ease-out, opacity 0.5s ease-out;
            text-align: left;
            background: var(--color-card);
            border: 1px solid var(--color-accent);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
            border-radius: 5px;
        }

        /* 1. When a section is targeted, SHOW IT */
        .hidden-section:target {
            max-height: 1000px;
            opacity: 1;
            padding: 15px 10px;
            margin-bottom: 15px; /* Space between open panel and bottom of card */
            transition: max-height 0.5s ease-in, opacity 0.5s ease-in;
        }

        /* 2. When #projects is targeted, HIDE ITS SIBLINGS */
        #projects:target ~ #about,
        /* 3. When #about is targeted, HIDE ITS SIBLINGS */
        #about:target ~ #projects {
            max-height: 0;
            opacity: 0;
            padding: 0 10px; 
            margin-bottom: 0;
            transition: max-height 0.5s ease-out, opacity 0.5s ease-out;
        }

        .hidden-section h2 {
            font-family: var(--font-heading);
            font-size: 1.1em;
            color: var(--color-accent);
            border-bottom: 1px solid var(--color-accent);
            padding-bottom: 5px;
            margin-top: 0;
            margin-bottom: 10px;
            text-transform: uppercase;
        }
        .hidden-section p {
            font-size: 0.9em;
        }
        .hidden-section p strong {
            color: var(--color-accent);
        }


        /* =================================
           V. GALLERY & LIGHTBOX 
           ================================= */
        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(60px, 1fr)); /* Smaller thumbnails */
            gap: 8px;
            margin-top: 10px;
        }
        .gallery-item img {
            width: 100%;
            height: 60px; /* Smaller height */
            object-fit: cover;
            border: 2px solid var(--color-accent);
            border-radius: 3px;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .gallery-item img:hover {
            transform: scale(1.05);
            box-shadow: 0 0 10px rgba(0, 188, 212, 0.7);
        }
        /* Lightbox styles remain for modal viewing */
        .lightbox-target {
            display: none;
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(13, 39, 63, 0.95);
            backdrop-filter: blur(5px);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .lightbox-target:target {
            display: flex;
        }
        .lightbox-content {
            max-width: 95%;
            max-height: 95%;
            text-align: center;
        }
        .lightbox-content img {
            max-width: 90vw;
            max-height: 80vh;
            border: 5px solid var(--color-accent);
            border-radius: 5px;
            box-shadow: 0 0 30px rgba(0, 188, 212, 0.8);
        }
        .lightbox-content .caption {
            margin-top: 10px;
            color: var(--color-text);
            font-style: italic;
            font-size: 0.9em;
        }
        .lightbox-close {
            position: absolute;
            top: 10px; /* Closer to top edge on mobile */
            right: 20px;
            color: var(--color-accent);
            font-size: 2.5em; /* Smaller close button */
            text-decoration: none;
            font-weight: 300;
            opacity: 0.9;
            transition: color 0.2s;
        }
        .lightbox-close:hover {
            color: #9b59b6;
        }

        /* =================================
           VI. DESKTOP/TABLET OVERRIDE (min-width: 768px)
           ================================= */
        @media (min-width: 768px) {
            .drawing-sheet {
                padding: 30px;
                display: grid;
                grid-template-columns: 1fr 2fr;
                gap: 20px;
            }
            .title-block {
                grid-column: 1 / 2;
                order: initial;
            }
            .content-area {
                grid-column: 2 / 3;
                order: initial;
            }
            .detail-panels-wrapper {
                grid-column: 1 / 3;
                order: initial;
                padding-top: 20px;
                border-top: 1px dashed rgba(255, 255, 255, 0.3);
            }
            .title-block h1 {
                font-size: 2.2em;
            }
            .profile-pic {
                width: 120px;
                height: 120px;
            }
            .contact-actions {
                justify-content: flex-start;
                flex-wrap: nowrap;
            }
            .contact-actions a {
                flex: 0 1 auto;
                max-width: 120px;
                padding: 10px 15px;
            }
            .spec-box {
                font-size: 0.9em;
            }
            .spec-box p {
                flex-wrap: nowrap;
            }
            .spec-box strong {
                flex-basis: auto;
            }
            .spec-box a {
                flex-basis: auto;
                text-align: right;
            }
        }
    </style>
</head>
<body>
    <div class="drawing-sheet">

        <div class="title-block">
            <img src="profile.jpg" alt="Heather Rosenau" class="profile-pic">
            <h1>HEATHER ROSENAU</h1>
            <p class="job-title">CAD Designer & Model Specialist</p>
        </div>

        <div class="content-area">

            <div class="contact-actions">
                <a href="https://linkedin.com/in/heatherrosenau" target="_blank">LinkedIn</a>
                <a href="#projects">Projects</a>
                <a href="#about">About Me</a>
                <a href="#" style="background: none; border: 1px dashed rgba(0, 188, 212, 0.5); color: var(--color-accent);">CLOSE</a>
            </div>
            
            <p>I am a highly detail-oriented **CAD professional** specializing in the transformation of conceptual designs into production-ready technical drawings and 3D models. My work ensures accuracy and manufacturability across diverse engineering and architectural domains.</p>

        </div>
        
        <div class="spec-box title-block" style="order: 4;">
            <p><strong>REVISION:</strong> 1.5</p>
            <p><strong>DATE:</strong> 2025/11/29</p>
            <p><strong>LOCATION:</strong> Denver, CO</p>
            <p><strong><a href="mailto:heather.rosenau@example.com">EMAIL</a>:</strong> heather.rosenau@example.com</p>
            <p><strong>PHONE:</strong> (555) 123‑4567</p>
        </div>

        <div class="detail-panels-wrapper">
            <div id="projects" class="hidden-section">
                <h2>Project Drawings & Models</h2>
                <div class="gallery">
                    <a href="#lb1" class="gallery-item">
                        <img src="project1.jpg" alt="Precision Gear Design - AutoCAD">
                    </a>
                    <a href="#lb2" class="gallery-item">
                        <img src="project2.jpg" alt="3D Model Render - SolidWorks">
                    </a>
                    <a href="#lb3" class="gallery-item">
                        <img src="project3.jpg" alt="Architectural Floor Plan - Revit">
                    </a>
                    <a href="#lb4" class="gallery-item">
                        <img src="project4.jpg" alt="Detailed Assembly View - Inventor">
                    </a>
                </div>
            </div>

            <div id="about" class="hidden-section">
                <h2>Technical Specification</h2>
                <p><strong>KEY SKILLS:</strong> Precision drafting, parametric modeling, GD&T application, clash detection, BIM coordination.</p>
                <p><strong>SOFTWARE SUITE:</strong> **AutoCAD**, **SolidWorks**, **Revit**, Inventor, Rhino 3D.</p>
                <p><strong>EXPERIENCE:</strong> 5+ years supporting mechanical engineering and industrial design teams in Denver, CO.</p>
            </div>
        </div>
    </div>

    <div id="lb1" class="lightbox-target">
        <div class="lightbox-content">
            <a href="#projects" class="lightbox-close" title="Close">&times;</a>
            <img src="project1.jpg" alt="Precision Gear Design - AutoCAD">
            <p class="caption">Precision Gear Design - AutoCAD</p>
        </div>
    </div>

    <div id="lb2" class="lightbox-target">
        <div class="lightbox-content">
            <a href="#projects" class="lightbox-close" title="Close">&times;</a>
            <img src="project2.jpg" alt="3D Model Render - SolidWorks">
            <p class="caption">3D Model Render - SolidWorks</p>
        </div>
    </div>

    <div id="lb3" class="lightbox-target">
        <div class="lightbox-content">
            <a href="#projects" class="lightbox-close" title="Close">&times;</a>
            <img src="project3.jpg" alt="Architectural Floor Plan - Revit">
            <p class="caption">Architectural Floor Plan - Revit</p>
        </div>
    </div>

    <div id="lb4" class="lightbox-target">
        <div class="lightbox-content">
            <a href="#projects" class="lightbox-close" title="Close">&times;</a>
            <img src="project4.jpg" alt="Detailed Assembly View - Inventor">
            <p class="caption">Detailed Assembly View - Inventor</p>
        </div>
    </div>
</body>
</html>
