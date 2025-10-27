<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import { projects } from '$lib/data/projects.js';

  gsap.registerPlugin(ScrollTrigger);

  onMount(() => {
    // Hero animation
    const tl = gsap.timeline({ defaults: { ease: 'power2.out', duration: 1 } });
    tl.from('.hero-text h1', { opacity: 0, y: 30 })
      .from('.hero-text p', { opacity: 0, y: 20, stagger: 0.15 }, '-=0.6')
      .from('.hero-nav a', { opacity: 0, y: 20, stagger: 0.1 }, '-=0.4')
      .from('.hero-image', { opacity: 0, x: 40 }, '-=1');

    // Scroll-triggered project animations
    gsap.utils.toArray('.project').forEach((section) => {
      const overlay = section.querySelector('.overlay');
      gsap.fromTo(
        overlay,
        { opacity: 0, y: 40 },
        {
          opacity: 1,
          y: 0,
          duration: 1,
          ease: 'power2.out',
          scrollTrigger: {
            trigger: section,
            start: 'top 80%',
            toggleActions: 'play none none none'
          }
        }
      );
    });
  });
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300&display=swap');

  main {
    font-family: 'Comfortaa', cursive;
    color: #222;
    background: #fff;
  }

  /* Hero section */
.hero {
  display: flex;
  justify-content: space-between;
  align-items: center; /* vertical alignment */
  padding: 2rem 5%; /* add horizontal padding for edge spacing */
  gap: 1rem;
  flex-wrap: wrap; /* allow stacking on narrow screens */
}

.hero-content {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  min-width: 200px; /* prevent nav links from collapsing too early */
}

.hero-content h1 {
  margin: 0;
  font-size: 2.5rem;
  color: #4169e1;
}

.hero-nav {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.hero-nav a {
  text-decoration: none;
  color: #4169e1;
  font-weight: 500;
}

.hero-nav a:hover {
  color: #2746b3;
}

.hero-image {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  object-fit: cover;
}

/* Mobile adjustments */
@media(max-width: 767px){
  .hero {
    flex-direction: column;
    align-items: flex-start;
    padding: 2rem 3%;
  }

  .hero-content {
    order: 2; /* so image can be first if desired */
  }

  .hero-image {
    margin-bottom: 1rem;
  }

  .hero-nav {
    gap: 1rem;
  }

  .hero-content h1 {
    font-size: 2rem;
  }
}

  /* Projects */
  #projects {
    margin: 0;
  }

  .project {
    position: relative;
    width: 100%;
    margin: 0; /* remove gaps between projects */
  }

  .project img {
    width: 100%;
    display: block;
    object-fit: cover;
  }

  .overlay {
    position: absolute;
    bottom: 0; /* overlay at bottom of image */
    left: 0;
    width: 100%;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    background: linear-gradient(to top, rgba(0,0,0,0.6), rgba(0,0,0,0.0));
    color: #fff;
    opacity: 0; /* GSAP animates to 1 */
  }

  .overlay h2 {
    margin: 0 0 0.3rem 0;
    font-size: 1.8rem;
  }

  .overlay p {
    margin: 0 0 0.5rem 0;
    font-size: 1rem;
    max-width: 600px;
  }

  .overlay a.button {
    align-self: flex-start;
    padding: 0.5rem 1rem;
    background: #4169e1;
    border-radius: 0.5rem;
    text-decoration: none;
    color: #fff;
    font-weight: 500;
    transition: background 0.2s;
  }

  .overlay a.button:hover {
    background: #2746b3;
  }

  /* Footer */
  footer {
    text-align: center;
    padding: 2rem;
    font-size: 0.9rem;
    color: #777;
  }

  footer a {
    color: #4169e1;
    text-decoration: none;
  }

  /* Mobile adjustments */
  @media (max-width: 767px) {
    .overlay {
      padding: 0.75rem;
    }

    .overlay h2 {
      font-size: 1.5rem;
    }

    .overlay p {
      font-size: 0.95rem;
    }

    .hero {
      flex-direction: column;
      align-items: flex-start;
    }

    .hero-nav {
      justify-content: flex-start;
    }
  }
</style>

<main>
<!-- Hero Intro -->
<section class="hero">
  <div class="hero-content">
    <h1>Drawing with Data</h1>
    <div class="hero-nav">
      <a href="https://www.etsy.com/uk/listing/xxxx" target="_blank">Buy Gospel Journey Planner</a>
      <a href="#projects">Portfolio</a>
      <a href="#services">My Services</a>
    </div>
  </div>
  <img src="/images/Chris Nov 24 Square.jpg" alt="Chris Woods" class="hero-image" />
</section>

  <!-- Project Gallery -->
  <section id="projects">
    {#each projects as project}
      <div class="project">
        <img src={project.image} alt={project.title} />
        <div class="overlay">
          <div>
            <h2>{project.title}</h2>
            <p>{project.description}</p>
          </div>
          {#if project.link}
            <a class="button" href={project.link} target="_blank">{project.featured ? 'Buy Print' : 'View Project'}</a>
          {/if}
        </div>
      </div>
    {/each}
  </section>

  <!-- Footer -->
  <footer>
    <p>© Chris Woods 2016–25 | <a href="https://html5up.net">HTML5 UP</a></p>
  </footer>
</main>
