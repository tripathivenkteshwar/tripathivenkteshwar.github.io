// === PARTICLE BACKGROUND ===
function initParticles() {
  const canvas = document.getElementById('particles-canvas');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  let particles = [];
  const resize = () => { canvas.width = window.innerWidth; canvas.height = window.innerHeight; };
  resize();
  window.addEventListener('resize', resize);
  
  class Particle {
    constructor() { this.reset(); }
    reset() {
      this.x = Math.random() * canvas.width;
      this.y = Math.random() * canvas.height;
      this.size = Math.random() * 2 + 0.5;
      this.speedX = (Math.random() - 0.5) * 0.5;
      this.speedY = (Math.random() - 0.5) * 0.5;
      this.opacity = Math.random() * 0.5 + 0.1;
    }
    update() {
      this.x += this.speedX;
      this.y += this.speedY;
      if (this.x < 0 || this.x > canvas.width || this.y < 0 || this.y > canvas.height) this.reset();
    }
    draw() {
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(102, 126, 234, ${this.opacity})`;
      ctx.fill();
    }
  }
  const count = Math.min(80, Math.floor(canvas.width * canvas.height / 15000));
  for (let i = 0; i < count; i++) particles.push(new Particle());

  function connectParticles() {
    for (let i = 0; i < particles.length; i++) {
      for (let j = i + 1; j < particles.length; j++) {
        const dx = particles[i].x - particles[j].x;
        const dy = particles[i].y - particles[j].y;
        const dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 150) {
          ctx.beginPath();
          ctx.strokeStyle = `rgba(102, 126, 234, ${0.08 * (1 - dist / 150)})`;
          ctx.lineWidth = 0.5;
          ctx.moveTo(particles[i].x, particles[i].y);
          ctx.lineTo(particles[j].x, particles[j].y);
          ctx.stroke();
        }
      }
    }
  }
  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    particles.forEach(p => { p.update(); p.draw(); });
    connectParticles();
    requestAnimationFrame(animate);
  }
  animate();
}

// === TYPING EFFECT ===
function initTyping() {
  const el = document.querySelector('.typing-text');
  if (!el) return;
  const titles = ['Senior Software Engineer', 'Backend Architect', 'Cloud & Microservices Engineer', 'System Design Expert'];
  let titleIndex = 0, charIndex = 0, isDeleting = false;
  function type() {
    const current = titles[titleIndex];
    el.textContent = isDeleting ? current.substring(0, charIndex--) : current.substring(0, charIndex++);
    if (!isDeleting && charIndex > current.length) { setTimeout(() => { isDeleting = true; type(); }, 2000); return; }
    if (isDeleting && charIndex < 0) { isDeleting = false; titleIndex = (titleIndex + 1) % titles.length; }
    setTimeout(type, isDeleting ? 30 : 80);
  }
  type();
}

// === NAVBAR ===
function initNavbar() {
  const navbar = document.querySelector('.navbar');
  const toggle = document.querySelector('.nav-toggle');
  const links = document.querySelector('.nav-links');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 50);
    // Floating CTA
    const cta = document.querySelector('.floating-cta');
    if (cta) cta.classList.toggle('visible', window.scrollY > 600);
    // Active nav link
    document.querySelectorAll('section[id]').forEach(section => {
      const top = section.offsetTop - 100;
      const id = section.id;
      const link = document.querySelector(`.nav-links a[href="#${id}"]`);
      if (link) link.classList.toggle('active', window.scrollY >= top && window.scrollY < top + section.offsetHeight);
    });
  });
  if (toggle) toggle.addEventListener('click', () => {
    links.classList.toggle('active');
    toggle.classList.toggle('open');
  });
  document.querySelectorAll('.nav-links a').forEach(a => a.addEventListener('click', () => links.classList.remove('active')));
}

// === SCROLL REVEAL ===
function initScrollReveal() {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => { if (entry.isIntersecting) { entry.target.classList.add('visible'); } });
  }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
}

// === SKILL BARS ===
function initSkillBars() {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.querySelectorAll('.skill-fill').forEach(bar => {
          bar.style.width = bar.dataset.width;
        });
      }
    });
  }, { threshold: 0.3 });
  document.querySelectorAll('.skill-category').forEach(el => observer.observe(el));
}

// === COUNTER ANIMATION ===
function animateCounters() {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting && !entry.target.dataset.animated) {
        entry.target.dataset.animated = 'true';
        const target = parseInt(entry.target.dataset.target);
        const suffix = entry.target.dataset.suffix || '';
        const prefix = entry.target.dataset.prefix || '';
        let current = 0;
        const increment = target / 60;
        const timer = setInterval(() => {
          current += increment;
          if (current >= target) { current = target; clearInterval(timer); }
          entry.target.textContent = prefix + Math.floor(current) + suffix;
        }, 20);
      }
    });
  }, { threshold: 0.5 });
  document.querySelectorAll('[data-target]').forEach(el => observer.observe(el));
}



// === INIT ===
document.addEventListener('DOMContentLoaded', () => {
  initParticles();
  initTyping();
  initNavbar();
  initScrollReveal();
  initSkillBars();
  animateCounters();
  initContactForm();
});
