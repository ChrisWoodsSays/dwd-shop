<script>
  import { onMount } from 'svelte';
  import { projects } from '$lib/data/projects.js';

  let featuredItems = [];
  const featuredTitle = 'Gospel Journey Planner';
  const featuredText = 'Beautifully designed visual guides to help you explore the Gospel story. Printed on high-quality art paper — perfect for gifts or study spaces.';
  const featuredLink = 'https://www.etsy.com/uk/listing/xxxx';

  onMount(async () => {
    const { gsap } = await import('gsap');
    const { ScrollTrigger } = await import('gsap/ScrollTrigger');
    gsap.registerPlugin(ScrollTrigger);

    gsap.from('.hero-title, .hero-nav a', {
      opacity: 0,
      y: 18,
      duration: 0.8,
      stagger: 0.12,
      ease: 'power2.out'
    });

    gsap.utils.toArray('.project').forEach((proj) => {
      const img = proj.querySelector('.project-image img');
      const content = proj.querySelector('.project-content');
      if (img) {
        gsap.from(img, {
          scale: 1.03,
          duration: 1.1,
          ease: 'power2.out',
          scrollTrigger: { trigger: proj, start: 'top 90%', toggleActions: 'play none none none' }
        });
      }
      if (content) {
        gsap.from(content, {
          opacity: 0,
          y: 36,
          duration: 0.9,
          ease: 'power2.out',
          scrollTrigger: { trigger: proj, start: 'top 85%', toggleActions: 'play none none none' }
        });
      }
    });

    featuredItems = [
      { image: '/images/JP1 - IMG_7063 Portrait.jpg', title: 'Gospel Journey Planner', description: 'Plan your journey through the Bible with clarity and ease.', link: 'https://www.etsy.com/uk/listing/xxxx' },
      { image: '/images/JP2 - IMG_7078.jpg', title: 'Data Visualization Print', description: 'Beautifully designed print for data enthusiasts.', link: 'https://www.etsy.com/uk/listing/yyyy' },
      { image: '/images/JP3 IMG_7068.jpg', title: 'Interactive Dashboard', description: 'Engage with your data interactively online.', link: 'https://www.etsy.com/uk/listing/zzzz' }
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
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 1rem;
    position: sticky;
    top: 0;
    background: #fff;
    z-index: 1000;
    padding-bottom: 1rem;
  }

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
    flex-wrap: nowrap; /* prevent unnecessary wrapping */
    font-weight: 600;
  }

  .hero-nav a {
    color: #4169e1;
    text-decoration: none;
    font-size: 0.98rem;
    white-space: nowrap;
  }

  .hero-nav a:hover {
    color: #2746b3;
  }

  .hero-buy {
    font-size: 0.85rem;
    padding: 0.5rem 0.8rem;
    background: #4169e1;
    color: #fff;
    text-decoration: none;
    border-radius: 6px;
    font-weight: 600;
    align-self: flex-start; 
    white-space: normal; /* allows wrapping on small screens */
    text-align: center;
  }

  .hero-buy:hover {
    background: #2746b3;
  }

  @media (max-width: 520px) {
    .hero-buy {
      font-size: 0.75rem;
      padding: 0.4rem 0.6rem;
    }
  }

  /* Intro full width */
  .hero-intro {
    margin: 3rem 0;
    width: 100%;
    color: #333;
    line-height: 1.48;
    font-size: 1.05rem;
  }

  /* ===== FEATURED ===== */
 .featured-wrapper {
  width: 100%;
  margin: 0;
  padding: 0;
}

.featured-container {
  display: flex;
  flex-direction: column;
  width: 100%;
  padding: 0;
}

/* Featured info: title + text + button */
.featured-info {
  display: flex;
  flex-direction: column;       /* always stack title + text */
  width: 100%;
  margin-bottom: 1.5rem;
}

/* Wrap title and text in one block, button in separate flex row for wide screens */
.featured-info-content {
  display: flex;
  flex-direction: column;      /* title + text stacked */
  max-width: 800px;
}

.featured-info h3 {
  margin: 0 0 0.5rem 0;
  font-size: 1.5rem;
  color: #222;
}

.featured-info p {
  margin: 0;
  font-size: 1rem;
  color: #333;
  line-height: 1.45;
}

/* Button: wide screens right of text */
.featured-info .button {
  display: inline-block;
  padding: 0.6rem 1.1rem;
  background: #4169e1;
  color: #fff;
  text-decoration: none;
  border-radius: 6px;
  font-weight: 600;
  margin-top: 1rem;
  align-self: flex-start;       /* default: below text, left-aligned */
}

.featured-info .button:hover {
  background: #2746b3;
}

/* Wide screens: place button right of text */
@media(min-width: 1100px) {
  .featured-info {
    flex-direction: row;
    justify-content: flex-start;
    align-items: flex-start;
    gap: 2rem;
  }
  .featured-info .button {
    align-self: flex-start;
    margin-top: 0;
  }
}

/* Medium screens: button below text, right-aligned */
@media(max-width: 1100px) {
  .featured-info {
    flex-direction: column;
    align-items: flex-start;
  }
  .featured-info .button {
    align-self: flex-end;
    margin-top: 0.5rem;
  }
}

/* Featured images grid */
.featured-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  width: 100%;
}

.featured-item {
  flex: 1 1 340px;
  display: flex;
  justify-content: center;
}

.featured-item img {
  width: 100%;
  height: auto;
  border-radius: 6px;
  box-shadow: 0 6px 20px rgba(0,0,0,0.06);
  display: block;
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

  .project:first-of-type { border-top: none; padding-top: 0; }

  .project.left-image { flex-direction: row; }
  .project.right-image { flex-direction: row-reverse; }

  .project-image { flex: 1 1 45%; min-width: 250px; min-height: 320px; overflow: hidden; border-radius: 4px; }
  .project-image img { width: 100%; height: 100%; object-fit: cover; border-radius: 4px; }

  .project-content { flex: 1 1 45%; display: flex; flex-direction: column; justify-content: space-between; }
  .project-content h2 { margin: 0 0 0.75rem 0; font-size: 1.6rem; color: #222; }
  .project-content p { margin: 0 0 0.5rem 0; color: #333; line-height: 1.45; font-size: 1rem; }
  .project-content a.button { padding: 0.5rem 0.9rem; background: #4169e1; color: #fff; border-radius: 4px; text-decoration: none; font-weight: 600; }
  .project-content a.button:hover { background: #2746b3; }

  /* ===== SERVICES ===== */
  #services {
    margin-top: 4rem;
    padding-top: 2rem;
    border-top: 1px solid rgba(0,0,0,0.08);
  }

  #services .services-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  #services img {
    width: 84px;
    height: 84px;
    border-radius: 50%;
    object-fit: cover;
  }

  #services p {
    margin-top: 1rem;
  }

  @media (max-width: 980px) {
    .project { flex-direction: column !important; }
    .project-image, .project-content { flex: 1 1 100%; }
    .project-image { min-height: 220px; }
    #services .services-header { flex-direction: column; align-items: flex-start; gap: 1rem; }
    #services img { width: 68px; height: 68px; }
  }

  @media (max-width: 520px) {
    .hero-title { font-size: 1.6rem; }
    .hero-intro { font-size: 1rem; }
    .featured-info p { max-width: 100%; margin-bottom: 0.5rem; }
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
    <a href={featuredLink} class="hero-buy" target="_blank" rel="noopener">Buy Gospel Journey Planner</a>
  </div>

  <!-- INTRO PARAGRAPH -->
  <p class="hero-intro">
    Data, insight and design, mixed with technology, enable us to see what's going on in the world,
    tell stories that matter, and make a difference. I help organisations communicate clearly with
    static and interactive visualisations — with an emphasis on Christian organisations, active travel,
    cycling, environment and social justice.
  </p>

  <!-- FEATURED SECTION -->
<div class="featured-wrapper">
  <div class="featured-container">
    <!-- Shared text + Buy button -->
<div class="featured-info">
  <div class="featured-info-content">
    <h3>{featuredTitle}</h3>
    <p>{featuredText}</p>
  </div>
  <a href={featuredLink} class="button" target="_blank" rel="noopener">Buy</a>
</div>


    <!-- Featured images grid -->
    <div class="featured-grid">
      {#each featuredItems as item}
        <div class="featured-item">
          <img src={item.image} alt={item.title} />
        </div>
      {/each}
    </div>
  </div>
</div>


  <!-- PROJECTS -->
  <section id="projects" aria-label="portfolio">
    {#each projects as project, i}
      <article class="project {i % 2 === 0 ? 'left-image' : 'right-image'}">

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



        <div class="project-image" aria-hidden="true">
          <img src={project.image} alt={project.title} />
        </div>


        
      </article>
    {/each}
  </section>

  <!-- SERVICES -->
  <section id="services">
    <div class="services-header">
      <h2>My Services</h2>
      <img src="/images/Chris Nov 24 Square.jpg" alt="Chris Woods" />
    </div>
    <p>Describe your services here. This section is linked from the top nav.</p>
  </section>

  <!-- FOOTER -->
  <footer>
    <p>© Chris Woods 2016–25</p>
  </footer>
</main>
