<script>
  import { onMount } from 'svelte';
  import { projects } from '$lib/data/projects.js';

  let featuredItems = [];
  const featuredTitle = 'Gospel Journey Planner';
  const featuredText = 'Beautifully designed visual guides to help you explore the Gospel story. Printed on high-quality art paper — perfect for gifts or study spaces.';
  const featuredLink = 'https://www.etsy.com/uk/listing/xxxx';

  onMount(async () => {
    // Dynamically import GSAP and ScrollTrigger (browser only)
    const { gsap } = await import('gsap');
    const { ScrollTrigger } = await import('gsap/ScrollTrigger');
    gsap.registerPlugin(ScrollTrigger);

    // Animate hero title and nav links
    gsap.from('.hero-title, .hero-nav a', {
      opacity: 0,
      y: 18,
      duration: 0.8,
      stagger: 0.12,
      ease: 'power2.out'
    });

    // Animate projects
    gsap.utils.toArray('.project').forEach((proj) => {
      const img = proj.querySelector('.project-image img');
      const content = proj.querySelector('.project-content');
      if (img) {
        gsap.from(img, {
          scale: 1.03,
          duration: 1.1,
          ease: 'power2.out',
          scrollTrigger: {
            trigger: proj,
            start: 'top 90%',
            toggleActions: 'play none none none'
          }
        });
      }
      if (content) {
        gsap.from(content, {
          opacity: 0,
          y: 36,
          duration: 0.9,
          ease: 'power2.out',
          scrollTrigger: {
            trigger: proj,
            start: 'top 85%',
            toggleActions: 'play none none none'
          }
        });
      }
    });

    // Set featured items
    featuredItems = [
      {
        image: '/images/JP1 - IMG_7063 Portrait.jpg',
        title: 'Gospel Journey Planner',
        description: 'Plan your journey through the Bible with clarity and ease.',
        link: 'https://www.etsy.com/uk/listing/xxxx'
      },
      {
        image: '/images/JP2 - IMG_7078.jpg',
        title: 'Data Visualization Print',
        description: 'Beautifully designed print for data enthusiasts.',
        link: 'https://www.etsy.com/uk/listing/yyyy'
      },
      {
        image: '/images/JP3 IMG_7068.jpg',
        title: 'Interactive Dashboard',
        description: 'Engage with your data interactively online.',
        link: 'https://www.etsy.com/uk/listing/zzzz'
      }
    ];
  });
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300&display=swap');

:global(body) {
  margin: 0;
  font-family: 'Comfortaa', cursive;
  background: #fff;
  color: #222;
}

main {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2.5rem 1.75rem;
}

/* ===== HERO ===== */
.hero-top {
  display: grid;
  grid-template-columns: 1fr auto;
  align-items: start;
  gap: 1rem;
  margin-bottom: 1.25rem;
  position: relative;
}

/* Keep title + nav stacked on the left */
.hero-left {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.hero-title {
  font-size: 2.2rem;
  color: #4169e1;
  margin: 0;
}

.hero-nav {
  display: flex;
  gap: 1.25rem;
  flex-wrap: wrap;
  font-weight: 600;
}

.hero-nav a {
  color: #4169e1;
  text-decoration: none;
  font-size: 0.98rem;
}

.hero-nav a:hover {
  color: #2746b3;
}

/* Top-right Buy button */
.hero-buy-button {
  display: inline-block;
  padding: 0.6rem 1.1rem;
  background: #4169e1;
  color: #fff;
  border-radius: 6px;
  font-weight: 600;
  text-decoration: none;
  align-self: start;
}

.hero-buy-button:hover {
  background: #2746b3;
}

/* ===== INTRO PARAGRAPH ===== */
.hero-intro {
  margin-bottom: 3rem;
  color: #333;
  line-height: 1.48;
  font-size: 1.05rem;
}

/* Full-width helper class for intro & featured-info */
.full-width {
  max-width: 1200px;
  margin: 0 auto 2rem auto;
}

/* ===== FEATURED SECTION ===== */
.featured-section {
  margin: 3rem 0;
}

.featured-grid {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 1rem;
  flex-wrap: nowrap;
}

.featured-item {
  flex: 1 1 0;
  display: flex;
  justify-content: center;
}

.featured-item img {
  width: 100%;
  max-width: 340px;
  height: auto;
  border-radius: 6px;
  box-shadow: 0 6px 20px rgba(0,0,0,0.06);
  display: block;
}

/* Shared text + button below all three */
.featured-info {
  text-align: center;
}

.featured-info h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.5rem;
  color: #222;
}

.featured-info p {
  margin: 0 0 1rem 0;
  color: #333;
  line-height: 1.45;
  font-size: 1rem;
}

.featured-info .button {
  display: inline-block;
  padding: 0.6rem 1.1rem;
  background: #4169e1;
  color: #fff;
  text-decoration: none;
  border-radius: 6px;
  font-weight: 600;
}

.featured-info .button:hover {
  background: #2746b3;
}

/* ===== PROJECTS ===== */
.project {
  display: flex;
  gap: 3rem;
  align-items: flex-start;
  margin: 4rem 0;
  padding: 2rem 0;
  border-top: 1px solid rgba(0,0,0,0.08);
}

.project:first-of-type {
  border-top: none;
  padding-top: 0;
}

.project.left-image {
  flex-direction: row;
}

.project.right-image {
  flex-direction: row-reverse;
}

.project-image {
  flex: 1 1 45%;
  min-width: 250px;
  min-height: 320px;
  overflow: hidden;
  border: 1px solid rgba(0,0,0,0.08);
  box-shadow: 0 8px 22px rgba(0,0,0,0.06);
  border-radius: 4px;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 4px;
  display: block;
}

.project-content {
  flex: 1 1 45%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.project-content h2 {
  margin: 0 0 0.75rem 0;
  font-size: 1.6rem;
  color: #222;
}

.project-content p {
  margin: 0 0 0.5rem 0;
  color: #333;
  line-height: 1.45;
  font-size: 1rem;
}

.project-content a.button {
  display: inline-block;
  padding: 0.5rem 0.9rem;
  background: #4169e1;
  color: #fff;
  text-decoration: none;
  border-radius: 4px;
  align-self: flex-start;
  font-weight: 600;
}

.project-content a.button:hover {
  background: #2746b3;
}

/* ===== SERVICES ===== */
#services {
  margin-top: 4rem;
  padding-top: 2rem;
  border-top: 1px solid rgba(0,0,0,0.08);
}

.services-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.hero-profile-right {
  width: 84px;
  height: 84px;
  border-radius: 50%;
  object-fit: cover;
}

/* ===== FOOTER ===== */
footer {
  margin-top: 4rem;
  color: #777;
  font-size: 0.95rem;
}

/* ===== RESPONSIVE ===== */
@media (max-width: 980px) {
  .project {
    flex-direction: column !important;
  }
  .project-image, .project-content {
    flex: 1 1 100%;
  }
  .project-image {
    min-height: 220px;
  }
}

@media (max-width: 900px) {
  .featured-grid {
    flex-wrap: wrap;
    gap: 1.25rem;
  }
  .featured-item {
    flex: 1 1 100%;
  }
  .services-header {
    flex-direction: column;
    align-items: flex-start;
  }
  .hero-profile-right {
    margin-top: 1rem;
  }
}

@media (max-width: 520px) {
  .hero-title {
    font-size: 1.6rem;
  }
  .hero-intro {
    font-size: 1rem;
  }
  .hero-profile-right {
    width: 68px;
    height: 68px;
  }
}

</style>


<main>
  <!-- HERO -->
  <div class="hero-top">
    <div class="hero-left">
      <h1 class="hero-title">Drawing with Data</h1>
      <nav class="hero-nav" aria-label="top nav">
        <a href="#projects">Portfolio</a>
        <a href="#services">My Services</a>
      </nav>
    </div>

    <!-- Top-right Buy button replaces profile image -->
    <a href={featuredLink} class="hero-buy-button" target="_blank" rel="noopener">
      Buy Gospel Journey Planner
    </a>
  </div>

  <!-- INTRO PARAGRAPH (full width like featured images) -->
  <p class="hero-intro full-width">
    Data, insight and design, mixed with technology, enable us to see what's going on in the world,
    tell stories that matter, and make a difference. I help organisations communicate clearly with
    static and interactive visualisations — with an emphasis on Christian organisations, active travel,
    cycling, environment and social justice.
  </p>

  <!-- Gospel Journey Planner text & button, full width -->
  <div class="featured-info full-width">
    <h3>{featuredTitle}</h3>
    <p>{featuredText}</p>
    <a href={featuredLink} class="button" target="_blank" rel="noopener">Buy</a>
  </div>

  <!-- Featured Section -->
  <section id="featured">
    <div class="featured-grid">
      {#each featuredItems as item}
        <div class="featured-item">
          <img src={item.image} alt={item.title} />
        </div>
      {/each}
    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects" aria-label="portfolio">
    {#each projects as project, i}
      <article class="project {i % 2 === 0 ? 'left-image' : 'right-image'}">
        <div class="project-image" aria-hidden="true">
          <img src={project.image} alt={project.title} />
        </div>
        <div class="project-content">
          <div><h2>{project.title}</h2></div>
          <div>
            <p>{project.description}</p>
            {#if project.link}
              <a class="button" href={project.link} target="_blank" rel="noopener">
                {project.featured ? 'Buy Print' : 'View Project'}
              </a>
            {/if}
          </div>
        </div>
      </article>
    {/each}
  </section>

  <!-- SERVICES (profile image moved here) -->
  <section id="services">
    <div class="services-header">
      <h2>My Services</h2>
      <img src="/images/Chris Nov 24 Square.jpg" alt="Chris Woods" class="hero-profile-right"/>
    </div>
    <p>Describe your services here. This section is linked from the top nav.</p>
  </section>

  <!-- FOOTER -->
  <footer>
    <p>© Chris Woods 2016–25</p>
  </footer>
</main>

