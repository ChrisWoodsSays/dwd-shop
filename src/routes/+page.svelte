<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import { projects } from '$lib/data/projects.js';
  let featuredItems = [];
    const featuredTitle = 'Gospel Journey Planner';
    const featuredText = 'Beautifully designed visual guides to help you explore the Gospel story. Printed on high-quality art paper — perfect for gifts or study spaces.';
  const featuredLink = 'https://www.etsy.com/uk/listing/xxxx';

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    gsap.from('.hero-title, .hero-nav a', {
      opacity: 0,
      y: 18,
      duration: 0.8,
      stagger: 0.12,
      ease: 'power2.out'
    });

    gsap.utils.toArray('.project').forEach((proj) => {
      gsap.from(proj.querySelector('.project-image img'), {
        scale: 1.03,
        duration: 1.1,
        ease: 'power2.out',
        scrollTrigger: {
          trigger: proj,
          start: 'top 90%',
          toggleActions: 'play none none none'
        }
      });
      gsap.from(proj.querySelector('.project-content'), {
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
    });


    // Example featured items array
    featuredItems = [
      {
        image: '/images/JP2.jpg',
        title: 'Gospel Journey Planner',
        description: 'Plan your journey through the Bible with clarity and ease.',
        link: 'https://www.etsy.com/uk/listing/xxxx'
      },
      {
        image: '/images/JP2.jpg',
        title: 'Data Visualization Print',
        description: 'Beautifully designed print for data enthusiasts.',
        link: 'https://www.etsy.com/uk/listing/yyyy'
      },
      {
        image: '/images/JP3.jpg',
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

  /* Profile image — always top-right */
.hero-profile {
  width: 84px;
  height: 84px;
  border-radius: 50%;
  object-fit: cover;
  position: absolute;
  top: 0;
  right: 0;
}

  .hero-intro {
    margin-bottom: 3rem;
    max-width: 76ch;
    color: #333;
    line-height: 1.48;
    font-size: 1.05rem;
  }

  /* ===== FEATURED SECTION ===== */
.featured-section {
  margin: 3rem 0;
}

.featured-grid {
  display: flex;
  justify-content: center; /* keeps it centered if space remains */
  align-items: flex-start;
  gap: 1rem; /* tighter gap between images */
  flex-wrap: nowrap; /* prevent wrapping on wide screens */
}

.featured-item {
  flex: 1 1 0;
  display: flex;
  justify-content: center;
}

.featured-item img {
  width: 100%;
  max-width: 340px; /* fits better across screens */
  height: auto;
  border-radius: 6px;
  box-shadow: 0 6px 20px rgba(0,0,0,0.06);
  display: block;
}

/* Shared text + button below all three */
.featured-info {
  margin-top: 1.5rem;
  text-align: center;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
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

/* Stack images vertically on smaller screens */
@media (max-width: 900px) {
  .featured-grid {
    flex-wrap: wrap;
    gap: 1.25rem;
  }
  .featured-item {
    flex: 1 1 100%;
  }
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
    .project-image { min-height: 220px; }

    /* Keep profile photo in top-right even when wrapping */
    .hero-top {
      display: block;
      position: relative;
    }

    .hero-profile {
      position: absolute;
      top: 0;
      right: 0;
    }
  }

  @media (max-width: 520px) {
    .hero-title { font-size: 1.6rem; }
    .hero-intro { font-size: 1rem; }
    .hero-profile { width: 68px; height: 68px; }
  }
</style>


<main>
  <!-- HERO -->
  <div class="hero-top">
    <div class="hero-left">
      <h1 class="hero-title">Drawing with Data</h1>
      <nav class="hero-nav" aria-label="top nav">
        <a href="https://www.etsy.com/uk/listing/xxxx" target="_blank" rel="noopener">Buy Gospel Journey Planner</a>
        <a href="#projects">Portfolio</a>
        <a href="#services">My Services</a>
      </nav>
    </div>

    <img src="/images/Chris Nov 24 Square.jpg" alt="Chris Woods" class="hero-profile" />
  </div>

  <!-- INTRO PARAGRAPH -->
  <p class="hero-intro">
    Data, insight and design, mixed with technology, enable us to see what's going on in the world,
    tell stories that matter, and make a difference. I help organisations communicate clearly with
    static and interactive visualisations — with an emphasis on Christian organisations, active travel,
    cycling, environment and social justice.
  </p>

<!-- Featured Section -->
<section id="featured">
  <div class="featured-grid">
    {#each featuredItems as item}
      <div class="featured-item">
        <img src={item.image} alt={item.title} />
      </div>
    {/each}
  </div>

  <!-- Shared title, text, and button below all images -->
  <div class="featured-info">
    <h3>{featuredTitle}</h3>
    <p>{featuredText}</p>
    <a href={featuredLink} class="button" target="_blank" rel="noopener">Buy</a>
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

  <!-- SERVICES -->
  <section id="services">
    <h2>My Services</h2>
    <p>Describe your services here. This section is linked from the top nav.</p>
  </section>

  <!-- FOOTER -->
  <footer>
    <p>© Chris Woods 2016–25</p>
  </footer>
</main>
