<template>
  <div id="app">
    <AppHeader :navItems="navItems" @scroll-to="scrollToSection" />
    <HeroSection :hero="heroData" @scroll-to="scrollToSection" />
    <AboutSection :about="aboutData" />
    <SkillsSection :skills="skillsData" />
    <ProjectsSection :projects="projectsData" />
    <SoftSide :soft="softData" />
    <ContactSection :contact="contactData" />
    <AppFooter :social="socialLinks" />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import HeroSection from './components/HeroSection.vue';
import AboutSection from './components/AboutSection.vue';
import SkillsSection from './components/SkillsSection.vue';
import ProjectsSection from './components/ProjectsSection.vue';
import SoftSide from './components/SoftSide.vue';
import ContactSection from './components/ContactSection.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    HeroSection,
    AboutSection,
    SkillsSection,
    ProjectsSection,
    SoftSide,
    ContactSection,
    AppFooter
  },
  data() {
    return {
      navItems: ['Home', 'About', 'Skills', 'Projects', 'SoftSide', 'Contact'],
      heroData: {
        name: 'Hosni Ranim',
        title: 'Full Stack Developer',
        subtitle: 'Master`s Degree in Intelligent Web Applications',
        cta: 'View My Work',
        resume: '/CV_Ranim Hosni.pdf'

      },
      aboutData: {
        image: require('@/assets/ranim.jpg'),
        description: 'Junior Full-Stack Web Developer specialized in web application development and CI/CD integration. Passionate about modern web technologies, with strong skills in Vue.js, Laravel, Node.js, and Jenkins. Curious, adaptable, and highly motivated, I am seeking an opportunity to contribute to innovative projects and continue developing my technical expertise.',
        highlights: [
          
        ]
      },
      skillsData: [
        { name: 'Vue.js', level: 90, category: 'frontend' },
        { name: 'JavaScript', level: 95, category: 'frontend' },
        { name: 'HTML/CSS', level: 90, category: 'frontend' },
        { name: 'Node.js', level: 85, category: 'backend' },
        { name: 'Python', level: 80, category: 'backend' },
        { name: 'MongoDB', level: 75, category: 'database' },
        { name: 'MySQL', level: 75, category: 'database' },
        { name: 'Git', level: 90, category: 'tools' },
        { name: 'Docker', level: 70, category: 'tools' },
        { name: 'Jenkins', level: 70, category: 'tools' }
      ],
      projectsData: [
        {
          id: 1,
          title: 'Intelligent platform',
          description: 'an innovative AI platform designed to make artificial intelligence accessible to everyone. It provides both an intuitive user interface and API integration, enabling developers, individuals, and local businesses to easily leverage AI-powered solutions.Participated in sprint planning, daily meetings, and iterative product deliveries.',
          image: require('@/assets/khabot.png'),
          tags: ['Vue.js', 'Node.js', 'MongoDB'],
          
          demo: 'https://khabot.com/w/'
        },
        {
          id: 2,
          title: 'Ririʼs Candles',
          description: 'E-commerce platform for a local candle business, featuring product listings, shopping cart, and secure checkout. Integrated DevOps practices through Docker containerization, Jenkins-based CI/CD pipelines, and automated deployment to improve reliability and streamline software delivery.',
          image: require('@/assets/riri.png'),
          tags: ['Laravel', 'Vuejs', 'MySQL'],
          github: 'https://github.com/ranimhosni/RiRi-s-Candle',
          demo: require('@/assets/2026-04-12 18-01-24.mp4')
        },
        {
          id: 3,
          title: 'Trendy store',
          description: ' Developed an E-commerce web application  following the Scrum methodology.Participated in sprint planning, team meetings, and iterative product deliveries, strengthening teamwork and collaboration skills.',
          image: require('@/assets/trendy.png'),
          tags: ['Vue.js', 'Node.js', 'MongoDB'],
          
        }
      ],
      softData: {
        items: [
          'Founding Member – Rotaract Sicca Kef Club -2022',
          'Assistant General Secretary – Rotaract Sicca Kef Club-2023',
          'Vice President – Rotaract Sicca Kef Club -2024',
          'Treasurer – ANT Club -2024',
          'Treasurer – IDER Club -2024',
          'Founder & Owner – Riri`s Candles (Founded and manage a handmade candle small business.) -2025'
        ]
        ,
        instagram: 'https://www.instagram.com/riris_candles/?next=%2F'
      },
      contactData: {
        email: 'ranimhasni06@gmail.com',
        phone: '+216 41 183 244',
        location: 'Tunisie'
      },
      socialLinks: [
        { name: 'GitHub', url: 'https://github.com/ranimhosni', icon: '📦' },
        { name: 'LinkedIn', url: 'https://www.linkedin.com/in/ranim-hosni-/', icon: '💼' },
        
      ]
    };
  },
  methods: {
    scrollToSection(section) {
      const element = document.getElementById(section.toLowerCase());
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
      }
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>