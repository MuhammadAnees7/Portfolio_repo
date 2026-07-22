/* ===== Anees Portfolio — Bootstrap Edition ===== */

// Typewriter effect
const phrases = [
  'Software Engineer',
  'Laravel Developer',
  'PHP Full Stack Developer',
  'REST API Developer',
  'OMS & CMS Specialist',
];

let phraseIdx = 0, text = '', deleting = false;
const typedEl = document.getElementById('typed-text');

function tick() {
  const current = phrases[phraseIdx % phrases.length];
  let delay;
  if (!deleting && text === current) {
    delay = 1800;
    deleting = true;
  } else if (deleting && text === '') {
    deleting = false;
    phraseIdx++;
    delay = 120;
  } else {
    text = deleting ? current.slice(0, text.length - 1) : current.slice(0, text.length + 1);
    if (typedEl) typedEl.textContent = text;
    delay = deleting ? 40 : 90;
  }
  setTimeout(tick, delay);
}
tick();

// Navbar scroll
const navbar = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  if (window.scrollY > 20) navbar.classList.add('scrolled');
  else navbar.classList.remove('scrolled');
});

// Mobile menu
const menuBtn = document.getElementById('menu-btn');
const mobileMenu = document.getElementById('mobile-menu');
if (menuBtn) {
  menuBtn.addEventListener('click', () => mobileMenu.classList.toggle('open'));
  mobileMenu.querySelectorAll('a').forEach(a => a.addEventListener('click', () => mobileMenu.classList.remove('open')));
}

// Active section highlight
const navLinks = document.querySelectorAll('.nav-link-custom');
const sections = ['about', 'skills', 'experience', 'projects', 'education', 'contact'];
const sectionObs = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const id = entry.target.id;
      navLinks.forEach(link => link.classList.toggle('active', link.getAttribute('href') === '#' + id));
    }
  });
}, { rootMargin: '-45% 0px -50% 0px' });
sections.forEach(id => { const el = document.getElementById(id); if (el) sectionObs.observe(el); });

// Scroll reveal
const revealObs = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('is-visible');
      revealObs.unobserve(entry.target);
    }
  });
}, { threshold: 0.12 });
document.querySelectorAll('.reveal').forEach(el => revealObs.observe(el));

// Back to top
const backTop = document.getElementById('back-to-top');
window.addEventListener('scroll', () => {
  backTop.style.display = window.scrollY > 500 ? 'grid' : 'none';
});
if (backTop) backTop.addEventListener('click', () => window.scrollTo({ top: 0, behavior: 'smooth' }));

// Contact form
const form = document.getElementById('contact-form');
if (form) {
  form.addEventListener('submit', (e) => {
    e.preventDefault();
    const btn = form.querySelector('button[type="submit"]');
    const original = btn.innerHTML;
    btn.innerHTML = '<i class="bi bi-check-circle"></i> Message Sent';
    btn.style.background = '#10b981';
    btn.style.color = '#070b14';
    form.reset();
    setTimeout(() => { btn.innerHTML = original; btn.style.background = ''; btn.style.color = ''; }, 3500);
  });
}
