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
            padding: 20px;
            /* Subtle grid background for drafting feel */
            background-image:
                linear-gradient(to right, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
            background-size: 20px 20px;
        }

        /* =================================
           II. MAIN CARD LAYOUT
           ================================= */
        .drawing-sheet {
            background: var(--color-card);
            border: 3px solid var(--color-accent); /* Stronger Border */
            border-radius: 5px;
            box-shadow: 0 0 15px rgba(0, 188, 212, 0.3);
            max-width: 800px;
            width: 100%;
            padding: 20px;
            display: grid;
            grid-template-columns: 1fr;
            gap: 20px;
        }
        
        /* Profile picture and Title Block styles remain the same for brevity */
        .title-block {
            text-align: center;
        }

        .title-block h1 {
            font-family: var(--font-heading);
            font-size: 2.2em;
            color: var(--color-accent);
            margin: 0 0 5px 0;
            line-height: 1;
            text-transform: uppercase;
        }

        .title-block .job-title {
            font-size: 1em;
            color: var(--color-text);
            margin-bottom: 20px;
        }

        .profile-pic {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            border: 4px solid var(--color-accent);
            box-shadow: 0 0 10px rgba(0, 188, 212, 0.5);
            margin-bottom: 20px;
            display: block;
            margin-left: auto;
            margin-right: auto;
        }

        /* Spec Box - Contact Info */
        .spec-box {
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 15px;
            background: rgba(0, 0, 0, 0.1);
            text-align: left;
            font-size: 0.9em;
            margin-top: 15px;
        }
        .spec-box p {
            margin: 5px 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .spec-box strong {
            color: var(--color-accent);
            margin-right: 10px;
        }
        .spec-box a {
            color: var(--color-text);
            text-decoration: none;
        }
        .spec-box a:hover {
            color: var(--color-accent);
        }

        /* Responsive grid for larger screens */
        @media (min-width: 768px) {
            .drawing-sheet {
                grid-template-columns: 1fr 2fr;
                padding: 30px;
            }
            .title-block {
                grid-column: 1 / 2;
            }
            .content-area {
                grid-column: 2 / 3;
            }
            .detail-panels-wrapper {
                grid-column: 1 / 3; /* Spans both columns at the bottom */
            }
        }
        
        /* =================================
           III. RADIO BUTTON HACK FOR TOGGLING
           ================================= */
        
        /* 1. Hide the actual radio inputs */
        .toggle-input {
            display: none;
        }

        /* 2. Style the <label> (which is linked to the radio) to look like a button */
        .contact-actions {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            justify-content: center;
        }

        .contact-actions label {
            padding: 10px 15px;
            background: var(--color-accent);
            color: var(--color-bg);
            text-decoration: none;
            border-radius: 3px;
            font-weight: 700;
            font-size: 0.9em;
            transition: background 0.3s, transform 0.2s;
            text-transform: uppercase;
            cursor: pointer;
            flex-grow: 1;
            text-align: center;
            max-width: 120px;
        }
        .contact-actions a { /* LinkedIn button remains standard anchor */
            padding: 10px 15px;
            background: #2980b9; /* Slightly different color for non-toggle */
            color: var(--color-text);
            text-decoration: none;
            border-radius: 3px;
            font-weight: 700;
            font-size: 0.9em;
            transition: background 0.3s, transform 0.2s;
            text-transform: uppercase;
            flex-grow: 1;
            text-align: center;
            max-width: 120px;
        }
        .contact-actions label:hover,
        .contact-actions a:hover {
            background: #0097a7;
            transform: translateY(-2px);
            color: var(--color-bg);
        }
        .contact-actions a:hover {
            background: #3498db;
        }


        /* 3. Style the label when the linked radio button is CHECKED (Active State) */
        #radio-projects:checked ~ .contact-actions label[for="radio-projects"],
        #radio-about:checked ~ .contact-actions label[for="radio-about"] {
            background: #9b59b6; /* Purple active color */
            color: var(--color-text);
        }
        
        /* 4. Hide all sections by default */
        .hidden-section {
            max-height: 0;
            overflow: hidden;
            opacity: 0;
            transition: max-height 0.5s ease-out, opacity 0.5s ease-out;
            text-align: left;
            border-top: 1px dashed rgba(255, 255, 255, 0.3);
            margin-top: 15px;
            padding-top: 0;
            box-sizing: border-box;
        }

        /* 5. Show the section only if its corresponding radio is checked */
        /* Use the General Sibling Combinator (~) to find the section next to the radio input */
        
        #radio-projects:checked ~ .detail-panels-wrapper #projects,
        #radio-about:checked ~ .detail-panels-wrapper #about {
            max-height: 1000px;
            opacity: 1;
            transition: max-height 0.5s ease-in, opacity 0.5s ease-in;
            padding-top: 15px;
        }
        
        /* Floating Appearance (Apply to the content of the panels) */
        .hidden-section h2 {
            font-family: var(--font-heading);
            font-size: 1.2em;
            color: var(--color-accent);
            border-bottom: 1px solid var(--color-accent);
            padding-bottom: 5px;
            margin-top: 0;
            margin-bottom: 15px;
            text-transform: uppercase;
        }
        .hidden-section p strong {
            color: var(--color-accent);
        }
        
        /* Floating Reset: Hide the border/padding when closed */
        .hidden-section:not([style*="max-height: 1000px"]) {
             border-top: none;
        }
        

        /* =================================
           IV. GALLERY & LIGHTBOX (CSS-Only) - Not modified from last version
           ================================= */
        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
            gap: 10px;
            margin-top: 15px;
        }
        .gallery-item img {
            width: 100%;
            height: 100px;
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

        /* Lightbox - Hidden by default */
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
            max-width: 90%;
            max-height: 90%;
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
        }
        .lightbox-close {
            position: absolute;
            top: 20px;
            right: 30px;
            color: var(--color-accent);
            font-size: 3.5em;
            text-decoration: none;
            font-weight: 300;
            opacity: 0.9;
            transition: color 0.2s;
        }
        .lightbox-close:hover {
            color: #9b59b6;
        }

        /* Responsive grid for smaller screens */
        @media (max-width: 767px) {
            .contact-actions {
                flex-wrap: wrap;
            }
            .contact-actions label, .contact-actions a {
                flex-grow: 1;
                max-width: 48%; /* Adjust for spacing */
            }
        }
    </style>
</head>
<body>
    <div class="drawing-sheet">

        <input type="radio" id="radio-projects" name="view-toggle" class="toggle-input">
        <input type="radio" id="radio-about" name="view-toggle" class="toggle-input">
        
        <div class="title-block">
            <img src="profile.jpg" alt="Heather Rosenau" class="profile-pic">
            <h1>Heather Rosenau</h1>
            <p class="job-title">CAD Designer & Model Specialist</p>

            <div class="spec-box">
                <p><strong>REVISION:</strong> 1.5</p>
                <p><strong>DATE:</strong> 2025/11/29</p>
                <p><strong>LOCATION:</strong> Denver, CO</p>
                <p><strong><a href="mailto:heather.rosenau@example.com">EMAIL</a>:</strong> heather.rosenau@example.com</p>
                <p><strong>PHONE:</strong> (555) 123‑4567</p>
            </div>
        </div>

        <div class="content-area">

            <div class="contact-actions">
                <a href="https://linkedin.com/in/heatherrosenau" target="_blank">LinkedIn</a>
                
                <label for="radio-projects">Projects</label>
                <label for="radio-about">About Me</label>
                
                <label for="close-view" style="background: none; border: 1px dashed rgba(0, 188, 212, 0.5); color: var(--color-accent); flex-grow: 0; max-width: 80px;">CLOSE</label>
            </div>
            
            <p>I am a highly detail-oriented **CAD professional** specializing in the transformation of conceptual designs into production-ready technical drawings and 3D models. My work ensures accuracy and manufacturability across diverse engineering and architectural domains.</p>

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
            <a href="#" class="lightbox-close" title="Close">&times;</a>
            <img src="project1.jpg" alt="Precision Gear Design - AutoCAD">
            <p class="caption">Precision Gear Design - AutoCAD</p>
        </div>
    </div>

    <div id="lb2" class="lightbox-target">
        <div class="lightbox-content">
            <a href="#" class="lightbox-close" title="Close">&times;</a>
            <img src="project2.jpg" alt="3D Model Render - SolidWorks">
            <p class="caption">3D Model Render - SolidWorks</p>
        </div>
    </div>

    <div id="lb3" class="lightbox-target">
        <div class="lightbox-content">
            <a href="#" class="lightbox-close" title="Close">&times;</a>
            <img src="project3.jpg" alt="Architectural Floor Plan - Revit">
            <p class="caption">Architectural Floor Plan - Revit</p>
        </div>
    </div>

    <div id="lb4" class="lightbox-target">
        <div class="lightbox-content">
            <a href="#" class="lightbox-close" title="Close">&times;</a>
            <img src="project4.jpg" alt="Detailed Assembly View - Inventor">
            <p class="caption">Detailed Assembly View - Inventor</p>
        </div>
    </div>
</body>
</html>
