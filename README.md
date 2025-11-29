<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Heather Rosenau | CAD Designer</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&family=Orbitron:wght@400;700&display=swap" rel="stylesheet">
  <style>
    /* Global and background (Kept) */
body {
  font-family: 'Montserrat', sans-serif;
  background-color: #0a2a43; /* blueprint blue */
  background-image:
    linear-gradient(135deg, rgba(255,255,255,0.03) 1px, transparent 1px),
    linear-gradient(45deg, rgba(255,255,255,0.03) 1px, transparent 1px);
  background-size: 40px 40px;
  color: #fdfdfd;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh; /* Changed to min-height for better content fit */
  margin: 0;
  padding: 20px; /* Added padding for small screens */
}

/* Card - Slimmed down for business card feel */
.card {
  position: relative;
  background: #2c3e50; /* steel gray */
  border: 2px solid #00bcd4; /* cyan accent border */
  border-radius: 10px;
  box-shadow: 0 6px 20px rgba(0,0,0,0.4);
  padding: 30px; /* Reduced padding */
  text-align: center;
  max-width: 500px; /* Reduced max-width for a more compact card */
  overflow: hidden;
  animation: float 4s ease-in-out infinite;
  width: 90%; /* Responsive width */
}

@keyframes float {
  0% { transform: translateY(0px); }
  50% { transform: translateY(-5px); } /* Reduced float distance */
  100% { transform: translateY(0px); }
}

/* Profile picture and CAD-style frame (Kept, but slightly smaller) */
.profile-wrapper {
  position: relative;
  display: inline-block;
  margin: 0 auto 15px auto;
}
.profile-pic {
  width: 100px; /* Reduced size */
  height: 100px; /* Reduced size */
  border-radius: 50%;
  border: 3px solid #00bcd4;
  display: block;
  transition: box-shadow 0.3s ease;
}
.profile-pic:hover {
  box-shadow: 0 0 10px rgba(0,188,212,0.7);
}
.profile-wrapper::before,
.profile-wrapper::after {
  content: "";
  position: absolute;
  width: 25px; /* Reduced size */
  height: 25px; /* Reduced size */
  border: 2px solid rgba(0,188,212,0.4);
}
.profile-wrapper::before {
  top: -8px;
  left: -8px;
  border-right: none;
  border-bottom: none;
}
.profile-wrapper::after {
  bottom: -8px;
  right: -8px;
  border-left: none;
  border-top: none;
}

/* Typography */
.card h1 {
  margin: 0 0 5px 0; /* Reduced margin */
  font-size: 1.8em; /* Reduced size */
  font-family: 'Orbitron', sans-serif;
  font-weight: 700;
  color: #00bcd4;
}
.card p {
  margin: 5px 0 15px 0; /* Reduced margin */
  font-size: 1em; /* Reduced size */
  color: #fdfdfd;
}
hr {
  border: 0;
  border-top: 1px solid rgba(0,188,212,0.3);
  margin: 15px 0;
}

/* Navigation buttons: Centered and simplified */
.contact {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px; /* Reduced gap */
  margin-top: 10px; /* Reduced margin */
}
.contact a {
  flex: 1 1 auto; /* Allow buttons to grow/shrink equally */
  max-width: 120px; /* Set a max width for buttons */
  display: inline-block;
  padding: 8px 15px; /* Reduced padding */
  background: #00bcd4;
  color: #0a2a43;
  text-decoration: none;
  border-radius: 5px;
  font-size: 0.85em; /* Reduced font size */
  cursor: pointer;
  transition: background 0.3s, transform 0.2s;
  font-weight: 700; /* Made buttons bolder */
}
.contact a:hover {
  background: #0097a7;
  transform: scale(1.05);
}
.contact a.active {
  background: #9b59b6;
  color: #fff;
}

/* Expandable sections (Kept) */
.hidden-section {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.5s ease-out, opacity 0.5s ease-out;
  margin-top: 15px; /* Reduced margin */
  text-align: left;
  opacity: 0;
}
.hidden-section.open {
  max-height: 1000px;
  opacity: 1;
  transition: max-height 0.5s ease-in, opacity 0.5s ease-in;
}
.hidden-section h2 {
  font-size: 1.1em; /* Reduced size */
  color: #00bcd4;
  font-family: 'Orbitron', sans-serif;
  margin-top: 0; /* Important for alignment */
}
.hidden-section p, .hidden-section ul {
  color: #fdfdfd;
  font-size: 0.95em; /* Reduced size */
}
.hidden-section ul {
  list-style: none; /* Removed default list style */
  padding-left: 0;
}

/* Portfolio gallery (Kept but smaller) */
.gallery {
  display: flex;
  flex-wrap: wrap;
  justify-content: center; /* Center images on mobile */
  gap: 8px; /* Reduced gap */
  margin-top: 10px;
}
.gallery img {
  width: 80px; /* Reduced size */
  height: 80px; /* Reduced size */
  object-fit: cover;
  border: 2px solid #00bcd4;
  border-radius: 5px;
  cursor: pointer;
  transition: transform 0.3s;
}
.gallery img:hover {
  transform: scale(1.1);
}
/* Removed expanded-img section to force use of lightbox */

/* Lightbox overlay (Kept) */
#lightbox {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: rgba(10,42,67,0.9); /* Darker background */
  backdrop-filter: blur(8px); /* Stronger blur */
  display: none;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}
#lightbox-content {
  position: relative;
  text-align: center;
  max-width: 90%;
}
#lightbox img {
  max-width: 100%; /* Better full-screen fit */
  max-height: 85vh; /* Limit height */
  border: 4px solid #00bcd4;
  border-radius: 10px;
  box-shadow: 0 0 25px rgba(0,188,212,0.7);
}
/* Arrows */
.arrow {
  font-size: 2.5em; /* Larger arrows */
  color: #00bcd4;
}

/* Divider (desktop only) and responsive layout - Simplified */
@media (min-width: 600px) { /* Reduced breakpoint for earlier desktop view */
  .card {
    display: flex;
    align-items: flex-start;
    text-align: left;
  }
  .profile-wrapper {
    margin: 0 20px 0 0; 
  }
  .card-content {
    flex: 1;
    padding-left: 20px; 
  }
  .divider {
    width: 1px; /* Thinner divider */
    background: rgba(0,188,212,0.4);
    margin: 0 15px; /* Less margin */
    height: 100%;
  }
  .contact {
    justify-content: flex-start; /* Align buttons to the left on desktop */
  }
  .contact a {
    flex: 0 1 auto; /* Natural size on desktop */
    max-width: none;
  }
}
  </style>
</head>
<body>
   <div id="lightbox" onclick="closeLightbox(event)">
  <div id="lightbox-content">
    <span id="arrow-left" class="arrow" onclick="prevImage(event)">&#10094;</span>
    <img id="lightbox-img" src="" alt="">
    <span id="arrow-right" class="arrow" onclick="nextImage(event)">&#10095;</span>
    <p id="lightbox-caption"></p>
  </div>
</div>

  <div class="card">
        <div class="profile-wrapper">
      <img src="profile.jpg" alt="Heather Rosenau" class="profile-pic">
    </div>

        <div class="divider"></div>

        <div class="card-content">
      <h1>Heather Rosenau</h1>
      <p>CAD Designer</p>
      <hr>
      <div class="contact">
  <a href="https://linkedin.com/in/heatherrosenau" target="_blank">LinkedIn</a>
  <a id="projectsBtn" onclick="toggleSection('projects', 'projectsBtn')">Projects</a>
  <a id="aboutBtn" onclick="toggleSection('about', 'aboutBtn')">About</a>
  <a id="contactBtn" onclick="toggleSection('contactInfo', 'contactBtn')">Contact</a> </div>

            <div id="projects" class="hidden-section">
        <h2>Portfolio Samples</h2>
        <div class="gallery">
          <img src="project1.jpg" alt="Precision Gear Design - AutoCAD" onclick="expandImage(this)">
          <img src="project2.jpg" alt="3D Model Render - SolidWorks" onclick="expandImage(this)">
          <img src="project3.jpg" alt="Architectural Floor Plan - Revit" onclick="expandImage(this)">
          <img src="project4.jpg" alt="Detailed Assembly View - Inventor" onclick="expandImage(this)">
        </div>
      </div>

            <div id="about" class="hidden-section">
        <h2>About Heather</h2>
        <p><strong>Specializing in precision drafting and 3D modeling.</strong> I bridge the gap between concept and fabrication, providing accurate technical documentation for engineering and architectural projects. Proficient in AutoCAD, SolidWorks, and Revit.</p>
      </div>
      <div id="contactInfo" class="hidden-section">
  <h2>Get in Touch</h2>
  <ul>
    <li>**Email:** <a href="mailto:heather.rosenau@example.com">heather.rosenau@example.com</a></li>
    <li>**Phone:** (555) 123‑4567</li>
    <li>**Location:** Denver, CO</li>
  </ul>
</div>
    </div>
  </div>

 <script>
  let currentIndex = 0;
  let galleryImages = [];

  function toggleSection(sectionId, btnId) {
    const sections = document.querySelectorAll('.hidden-section');
    const buttons = document.querySelectorAll('.contact a');
    const section = document.getElementById(sectionId);
    const button = document.getElementById(btnId);

    // If the target section is already open, close it.
    if (section.classList.contains('open')) {
      section.classList.remove('open');
      button.classList.remove('active');
      return; // Exit function
    }

    // Close all other sections and remove active class from all buttons
    sections.forEach(sec => sec.classList.remove('open'));
    buttons.forEach(btn => btn.classList.remove('active'));

    // Open the target section and set button active
    section.classList.add('open');
    button.classList.add('active');
  }

  function expandImage(img) {
    // Close all sections when opening the lightbox (for a cleaner look)
    document.querySelectorAll('.hidden-section').forEach(sec => sec.classList.remove('open'));
    document.querySelectorAll('.contact a').forEach(btn => btn.classList.remove('active'));


    galleryImages = Array.from(document.querySelectorAll('.gallery img'));
    currentIndex = galleryImages.indexOf(img);

    const lightbox = document.getElementById('lightbox');
    const lightboxImg = document.getElementById('lightbox-img');
    const lightboxCaption = document.getElementById('lightbox-caption');

    lightboxImg.src = img.src;
    lightboxImg.alt = img.alt;
    // Use the alt text as the caption
    lightboxCaption.textContent = img.alt;

    lightbox.style.display = 'flex';
  }

  function closeLightbox(event) {
    // Only close if the click is on the lightbox background, not the content or arrows
    if (event && event.target.id === 'lightbox') {
      document.getElementById('lightbox').style.display = 'none';
    } else if (!event) { // For keyboard 'Escape' key
      document.getElementById('lightbox').style.display = 'none';
    }
  }

  function prevImage(event) {
    if (event) event.stopPropagation();
    currentIndex = (currentIndex - 1 + galleryImages.length) % galleryImages.length;
    showImage();
  }

  function nextImage(event) {
    if (event) event.stopPropagation();
    currentIndex = (currentIndex + 1) % galleryImages.length;
    showImage();
  }

  function showImage() {
    const img = galleryImages[currentIndex];
    const lightboxImg = document.getElementById('lightbox-img');
    const lightboxCaption = document.getElementById('lightbox-caption');

    lightboxImg.src = img.src;
    lightboxImg.alt = img.alt;
    lightboxCaption.textContent = img.alt;
  }

  // Keyboard navigation (Kept)
  document.addEventListener('keydown', function(e) {
    const lightbox = document.getElementById('lightbox');
    if (lightbox.style.display === 'flex') {
      if (e.key === 'ArrowLeft') {
        prevImage();
      } else if (e.key === 'ArrowRight') {
        nextImage();
      } else if (e.key === 'Escape') {
        closeLightbox();
      }
    }
  });
</script>
</body>
</html>
