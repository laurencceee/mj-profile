<template>
  <div
    class="scroll-container"
    @scroll="handleScroll"
    ref="scrollContainer"
    :class="{ dark: isDark }"
  >
    <!-- PROFILE SECTION -->
    <section
      class="section profile-section"
      :class="{ 'fade-out': scrolledDown, 'fade-in': !scrolledDown }"
      ref="section1"
    >
      <div class="profile-card">
        <img
          src="./assets/mj.jpg"
          alt="Mary Jorge Tagle"
          class="profile-pic"
        />
        <h1 class="profile-name">Mary Jorge Tagle</h1>
        <p class="profile-title">
          Bachelor of Arts in Communication -<br />
          <em>Fresh Graduate</em>
        </p>

        <div class="btn-group">
          <button @click="viewResume" class="btn btn-primary">View Resume</button>
          <a :href="resumeLink" download class="btn btn-outline">Download Resume</a>
        </div>
      </div>
    </section>

    <!-- EXPERIENCE SECTION -->
    <section
      class="section experience-section"
      :class="{ 'fade-in': scrolledDown, 'fade-out': !scrolledDown }"
      ref="section2"
    >
      <h2 class="section-title">Experience & Achievements</h2>
      <div class="experience-list">
        <article class="experience-item">
          <div class="experience-date">2021 - 2025</div>
          <h3 class="experience-role">Legislative Assistant</h3>
          <p class="experience-company">Pasig City Hall - Office of Angelu De Leon</p>
          <p class="experience-desc">
            Supported legislative processes and community initiatives under the Pasig City government.
          </p>
        </article>

        <article class="experience-item">
          <div class="experience-date">2024 - 2025</div>
          <h3 class="experience-role">President</h3>
          <p class="experience-company">Student Coordinating Body</p>
          <p class="experience-desc">
            Led student governance and coordinated activities to enhance campus life and communication.
          </p>
        </article>

        <article class="experience-item">
          <div class="experience-date">2025</div>
          <h3 class="experience-role">Communication Awards</h3>
          <p class="experience-company">Pasig Catholic College</p>
          <p class="experience-desc">
            Recognized for outstanding performance in communication and media production.
          </p>
        </article>

        <article class="experience-item">
          <div class="experience-date">2025</div>
          <h3 class="experience-role">Best Student</h3>
          <p class="experience-company">Pasig Catholic College</p>
          <p class="experience-desc">
            Awarded Best Student for academic excellence and leadership contributions.
          </p>
        </article>

        <article class="experience-item">
          <div class="experience-date">2025</div>
          <h3 class="experience-role">Top Overall</h3>
          <p class="experience-company">Pasig Catholic College</p>
          <p class="experience-desc">
            Graduated top overall with honors in Bachelor of Communication program.
          </p>
        </article>
      </div>
    </section>

    <!-- Floating Dark Mode Toggle -->
    <button class="dark-mode-toggle" @click="toggleDarkMode" :aria-label="isDark ? 'Switch to Light Mode' : 'Switch to Dark Mode'">
      <template v-if="isDark">
        <!-- Sun icon for Light Mode -->
        <svg xmlns="http://www.w3.org/2000/svg" class="icon" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
          <circle cx="12" cy="12" r="5" stroke="currentColor" stroke-width="2" fill="yellow"/>
          <path stroke-linecap="round" stroke-linejoin="round" d="M12 1v2m0 18v2m11-11h-2M3 12H1m16.364-6.364l-1.414 1.414M6.05 17.95l-1.414 1.414m12.728 0l1.414 1.414M6.05 6.05L4.636 4.636" />
        </svg>
      </template>
      <template v-else>
        <!-- Moon icon for Dark Mode -->
        <svg xmlns="http://www.w3.org/2000/svg" class="icon" fill="currentColor" viewBox="0 0 24 24" stroke="none">
          <path d="M21 12.79A9 9 0 0112.21 3a7 7 0 000 14 9 9 0 018.79-4.21z" />
        </svg>
      </template>
    </button>
  </div>
</template>

<script>

export default {
  name: 'AppleStyleProfile',
  data() {
    return {
      resumeLink:
        'https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf',
      scrolledDown: false,
      isDark: false,
    }
  },
  mounted() {
    this.$refs.scrollContainer.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    this.$refs.scrollContainer.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    viewResume() {
      window.open(this.resumeLink, '_blank')
    },
    handleScroll() {
      const scrollTop = this.$refs.scrollContainer.scrollTop
      const windowHeight = window.innerHeight
      this.scrolledDown = scrollTop >= windowHeight / 2
    },
    toggleDarkMode() {
      this.isDark = !this.isDark
    },
  },
}
</script>

<style>
/* Scroll container */

/* === Dark Mode Variables === */
:root {
  --background-light: #fafafa;
  --background-dark: #1c1c1e;
  --card-light: #ffffff;
  --card-dark: #2c2c2e;
  --text-light: #1d1d1f;
  --text-dark: #f0f0f5;
  --shadow-light: rgba(0, 0, 0, 0.1);
  --shadow-dark: rgba(0, 0, 0, 0.6);
  --accent-blue: #007aff;
}

/* Scroll container background and text colors */
.scroll-container {
  background: var(--background-light);
  color: var(--text-light);
  transition: background-color 0.3s ease, color 0.3s ease;
}

.scroll-container.dark {
  background: var(--background-dark);
  color: var(--text-dark);
}

/* Card backgrounds and shadows */
.section {
  background: var(--card-light);
  box-shadow: 0 30px 60px var(--shadow-light);
  transition: background-color 0.3s ease, box-shadow 0.3s ease, color 0.3s ease;
}

.scroll-container.dark .section {
  background: var(--card-dark);
  box-shadow: 0 30px 60px var(--shadow-dark);
}

/* Buttons */
.btn {
  background-color: var(--accent-blue);
  color: white;
  box-shadow: 0 4px 14px rgb(13 110 253 / 0.3);
}

.btn:hover {
  background-color: #005ecb;
  box-shadow: 0 8px 30px rgb(0 122 255 / 0.5);
}

.btn-outline {
  background: transparent;
  color: var(--accent-blue);
  border: 2px solid var(--accent-blue);
}

.btn-outline:hover {
  background-color: var(--accent-blue);
  color: white;
  box-shadow: 0 8px 30px rgb(0 122 255 / 0.5);
}

/* Experience card shadows on hover */
.experience-item:hover {
  box-shadow:
    0 20px 40px var(--accent-blue),
    inset 0 0 3px rgba(0, 122, 255, 0.06);
}

/* Floating dark mode toggle button */
.dark-mode-toggle {
  position: fixed;
  bottom: 25px;
  right: 25px;
  width: 56px;
  height: 56px;
  background: var(--card-light);
  border-radius: 50%;
  border: none;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition:
    background-color 0.3s ease,
    box-shadow 0.3s ease,
    color 0.3s ease;
  color: var(--accent-blue);
  z-index: 1000;
}

.scroll-container.dark .dark-mode-toggle {
  background: var(--card-dark);
  color: #f5f5f7;
  box-shadow: 0 4px 12px rgba(0,0,0,0.7);
}

.dark-mode-toggle:hover {
  box-shadow: 0 6px 20px var(--accent-blue);
}

/* Icon size */
.dark-mode-toggle .icon {
  width: 24px;
  height: 24px;
  stroke: currentColor;
  fill: currentColor;
}

.scroll-container {
  height: 100vh;
  overflow-y: auto;
  scroll-behavior: smooth;
  background: #fafafa;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  color: #1d1d1f;
}

/* Fullscreen sections, flex center */
.section {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 3rem 1.5rem;
  box-sizing: border-box;
  transition: opacity 0.6s ease, transform 0.6s ease;
  background: white;
  max-width: 720px;
  margin: 0 auto;
  border-radius: 20px;
  box-shadow: 0 30px 60px rgb(0 0 0 / 0.1);
}

/* Fade animations */
.fade-in {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}
.fade-out {
  opacity: 0;
  transform: translateY(-40px);
  pointer-events: none;
}

/* ===== PROFILE SECTION ===== */
.profile-card {
  text-align: center;
  max-width: 360px;
  width: 100%;
  padding: 0 1rem;
}

.profile-pic {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  box-shadow:
    0 15px 30px rgb(0 0 0 / 0.15),
    inset 0 0 10px rgb(255 255 255 / 0.6);
  margin-bottom: 2rem;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.profile-pic:hover {
  transform: scale(1.05);
}

.profile-name {
  font-weight: 700;
  font-size: 2.8rem;
  margin-bottom: 0.3rem;
  letter-spacing: -0.015em;
  color: #000;
}

.profile-title {
  font-weight: 400;
  font-size: 1.1rem;
  color: #636366;
  margin-bottom: 2.5rem;
  font-style: italic;
}

/* Buttons container */
.btn-group {
  display: flex;
  justify-content: center;
  gap: 1.2rem;
}

.btn {
  font-weight: 600;
  font-size: 1.05rem;
  padding: 0.8rem 2rem;
  border-radius: 12px;
  cursor: pointer;
  border: none;
  user-select: none;
  transition: background-color 0.25s ease, box-shadow 0.25s ease;
  box-shadow: 0 4px 14px rgb(13 110 253 / 0.3);
  background-color: #007aff;
  color: white;
  font-family: inherit;
  -webkit-font-smoothing: antialiased;
}

.btn:hover {
  background-color: #005ecb;
  box-shadow: 0 8px 30px rgb(0 122 255 / 0.5);
}

.btn:focus-visible {
  outline: 3px solid #007aff;
  outline-offset: 2px;
}

.btn-outline {
  background: transparent;
  color: #007aff;
  border: 2px solid #007aff;
  box-shadow: none;
}

.btn-outline:hover {
  background-color: #007aff;
  color: white;
  box-shadow: 0 8px 30px rgb(0 122 255 / 0.5);
}

/* ===== EXPERIENCE SECTION ===== */
.section-title {
  font-size: 2.8rem;
  font-weight: 700;
  color: #1c1c1e;
  margin-bottom: 3rem;
  letter-spacing: 0.03em;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}

/* Experience list container */
.experience-list {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 2.8rem;
}

/* Experience item card */
.experience-item {
  background: #f5f5f7;
  border-radius: 20px;
  padding: 2rem 2.5rem;
  box-shadow:
    0 10px 30px rgb(0 0 0 / 0.07),
    inset 0 0 2px rgb(0 0 0 / 0.03);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: default;
  user-select: none;
}

.experience-item:hover {
  transform: translateY(-8px);
  box-shadow:
    0 20px 40px rgb(0 122 255 / 0.15),
    inset 0 0 3px rgb(0 122 255 / 0.06);
}

/* Date text */
.experience-date {
  font-size: 0.9rem;
  font-weight: 500;
  color: #8e8e93;
  margin-bottom: 0.5rem;
  font-style: italic;
  letter-spacing: 0.02em;
}

/* Role title */
.experience-role {
  font-weight: 700;
  font-size: 1.4rem;
  margin-bottom: 0.3rem;
  color: #000;
  letter-spacing: 0.01em;
}

/* Company text */
.experience-company {
  font-weight: 500;
  font-size: 1rem;
  color: #3c3c4399;
  margin-bottom: 1rem;
}

/* Description */
.experience-desc {
  font-size: 1rem;
  line-height: 1.5;
  color: #2c2c2e;
}

/* Responsive for small screens */
@media (max-width: 480px) {
  .section {
    padding: 2rem 1.5rem;
    border-radius: 14px;
    height: auto;
    min-height: 100vh;
  }

  .profile-card {
    max-width: 100%;
  }

  .profile-pic {
    width: 130px;
    height: 130px;
  }

  .btn-group {
    flex-direction: column;
    gap: 1rem;
  }

  .btn {
    width: 100%;
  }

  .experience-item {
    padding: 1.5rem 1.8rem;
  }
}

</style>