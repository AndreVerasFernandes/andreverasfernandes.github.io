<script setup>
import { computed, onMounted, ref } from 'vue';

const language = ref('pt');
const theme = ref('light');
const activeSkill = ref('Languages');

const skillTabs = ['Languages', 'Backend', 'Frontend', 'Databases', 'DevOps', 'Practices', 'Tools'];

const skillMap = {
  Languages: ['Python', 'JavaScript', 'Java', 'C', 'HTML', 'CSS', 'SQL', 'PL/SQL'],
  Backend: ['Node.js', 'Flask'],
  Frontend: ['React', 'Vue.js'],
  Databases: ['Oracle', 'MySQL', 'PostgreSQL', 'MongoDB', 'Database Design'],
  DevOps: ['GCP', 'Docker'],
  Practices: ['OOP', 'REST APIs', 'Scrum', 'Agile'],
  Tools: ['Git', 'Jira', 'Postman', 'DBeaver', 'Power BI', 'Linux']
};

const skillIcons = {
  Python: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg',
  JavaScript: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg',
  Java: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg',
  C: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/c/c-original.svg',
  HTML: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg',
  CSS: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg',
  'Node.js': 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg',
  Flask: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/flask/flask-original.svg',
  React: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg',
  'Vue.js': 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg',
  Oracle: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/oracle/oracle-original.svg',
  MySQL: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg',
  PostgreSQL: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg',
  MongoDB: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mongodb/mongodb-original.svg',
  SQL: 'https://icon.icepanel.io/Technology/svg/SQL-Developer.svg',
  'PL/SQL': 'https://icon.icepanel.io/Technology/svg/Oracle.svg',
  Jira: 'https://icon.icepanel.io/Technology/svg/Jira.svg',
  DBeaver: 'https://icon.icepanel.io/Technology/svg/DBeaver.svg',
  Postman: 'https://icon.icepanel.io/Technology/svg/Postman.svg',
  GCP: 'https://icon.icepanel.io/Technology/svg/Google-Cloud.svg',
  'Power BI': 'https://upload.wikimedia.org/wikipedia/commons/c/cf/New_Power_BI_Logo.svg',
  Docker: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg',
  Git: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg',
  Linux: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg'
};

const genericSkillIcon = 'https://cdn.jsdelivr.net/gh/twitter/twemoji/assets/svg/1f5a5.svg';

const profileLinks = {
  github: 'https://github.com/AndreVerasFernandes',
  linkedin: 'https://www.linkedin.com/in/andre-veras-fernandes/'
};

const i18n = {
  pt: {
    utilityTheme: 'Tema',
    utilityLang: 'Idioma',
    heroEyebrow: 'Engenheiro de Software',
    heroTitle: 'Ola, eu sou Andre Veras Fernandes',
    heroLead:
      'Desenvolvo plataformas web escalaveis com foco em performance, qualidade e evolucao continua. Trabalho entre backend, frontend e dados para transformar requisitos complexos em produtos confiaveis.',
    heroCta: 'Ver projetos',
    aboutTitle: 'Sobre',
    aboutText:
      'Sou engenheiro de software com experiencia em APIs, dados, cloud e desenvolvimento full stack. Tenho facilidade para aprender rapido, colaborar em times ageis e entregar solucoes orientadas a negocio.',
    workTitle: 'Experiencia',
    projectsTitle: 'Projetos',
    projectsCta: 'Abrir no GitHub',
    skillsTitle: 'Skills',
    contactTitle: 'Contato',
    contactText: 'Fale comigo por email ou pelas redes abaixo.',
    emailPlaceholder: 'Seu email',
    messagePlaceholder: 'Sua mensagem',
    send: 'Enviar mensagem',
    nav: {
      home: 'Inicio',
      about: 'Sobre',
      work: 'Experiencia',
      projects: 'Projetos',
      contact: 'Contato'
    },
    tabLabels: {
      Languages: 'Linguagens',
      Backend: 'Backend',
      Frontend: 'Frontend',
      Databases: 'Bancos',
      DevOps: 'DevOps',
      Practices: 'Praticas',
      Tools: 'Ferramentas'
    },
    work: [
      {
        company: 'Tribunal de Contas da União',
        role: 'Estagiário',
        employerLine: 'Tribunal de Contas da União · Estágio',
        period: 'jan de 2025 - o momento · 1 ano 3 meses',
        location: 'Remoto',
        bullets: [
          'Responsável pelo desenvolvimento e manutenção de aplicações Web, voltadas para auxiliar os procedimentos do Tribunal.',
          'Utilização do Oracle APEX para construção dos sistemas, modelagem de bancos de dados relacionais, construção e manutenção de queries SQL para geração de relatórios; Construção e manutenção de pacotes PL/SQL, de Dashboards e APIs.',
          'Utilização de metodologias ágeis no fluxo de trabalho.'
        ]
      }
    ],
    educationTitle: 'Formação Acadêmica',
    education: [
      {
        institution: 'Centro Universitário Senac',
        degree: 'Bacharelado em Engenharia, Engenharia de Computação',
        period: 'fev de 2022 - 2026'
      },
      {
        institution: 'Open Source Society University',
        degree: 'Ciência da Computação',
        period: ''
      }
    ],
    projects: [
      {
        name: 'Pipelines',
        desc: 'Colecao de automacoes e scripts em Python para processamento e organizacao de dados.',
        stack: ['Python', 'Automation'],
        link: 'https://github.com/AndreVerasFernandes/Pipelines'
      },
      {
        name: 'Order-API',
        desc: 'API de pedidos desenvolvida como desafio tecnico com foco em estrutura, validacoes e fluxo REST.',
        stack: ['JavaScript', 'REST APIs', 'Node.js'],
        link: 'https://github.com/AndreVerasFernandes/Order-API'
      },
      {
        name: 'Tomografo',
        desc: 'Projeto acadêmico focado em processamento e análise de dados em ambiente de notebooks.',
        stack: ['Python', 'Jupyter Notebook'],
        link: 'https://github.com/AndreVerasFernandes/Tomografo'
      }
    ]
  },
  en: {
    utilityTheme: 'Theme',
    utilityLang: 'Language',
    heroEyebrow: 'Software Engineer',
    heroTitle: 'Hi, I am Andre Veras Fernandes',
    heroLead:
      'I build scalable web platforms focused on performance, quality, and continuous improvement. I work across backend, frontend, and data to turn complex requirements into reliable products.',
    heroCta: 'See projects',
    aboutTitle: 'About',
    aboutText:
      'I am a software engineer experienced in APIs, data, cloud, and full-stack development. I am a fast learner, team-oriented, and focused on delivering business-driven solutions.',
    workTitle: 'Work Experience',
    projectsTitle: 'Projects',
    projectsCta: 'Open on GitHub',
    skillsTitle: 'Skills',
    contactTitle: 'Get in Touch',
    contactText: 'Reach me by email or through the networks below.',
    emailPlaceholder: 'Your email',
    messagePlaceholder: 'Your message',
    send: 'Send message',
    nav: {
      home: 'Home',
      about: 'About',
      work: 'Work',
      projects: 'Projects',
      contact: 'Contact'
    },
    tabLabels: {
      Languages: 'Languages',
      Backend: 'Backend',
      Frontend: 'Frontend',
      Databases: 'Databases',
      DevOps: 'DevOps',
      Practices: 'Practices',
      Tools: 'Tools'
    },
    work: [
      {
        company: 'Federal Court of Accounts (TCU)',
        role: 'Intern',
        employerLine: 'Federal Court of Accounts · Internship',
        period: 'Jan 2025 - Present · 1 year 3 months',
        location: 'Remote',
        bullets: [
          'Responsible for developing and maintaining Web applications aimed at supporting Court procedures.',
          'Use of Oracle APEX for system development, relational database modeling, SQL query creation and maintenance for reports; development and maintenance of PL/SQL packages, dashboards, and APIs.',
          'Use of agile methodologies in the development workflow.'
        ]
      }
    ],
    educationTitle: 'Education',
    education: [
      {
        institution: 'Centro Universitário Senac',
        degree: 'Bachelor of Engineering, Computer Engineering',
        period: 'Feb 2022 - 2026'
      },
      {
        institution: 'Open Source Society University',
        degree: 'Computer Science',
        period: ''
      }
    ],
    projects: [
      {
        name: 'Pipelines',
        desc: 'Collection of Python automations and scripts for data processing and workflow organization.',
        stack: ['Python', 'Automation'],
        link: 'https://github.com/AndreVerasFernandes/Pipelines'
      },
      {
        name: 'Order-API',
        desc: 'Order API technical challenge focused on architecture, validations, and REST flow design.',
        stack: ['JavaScript', 'REST APIs', 'Node.js'],
        link: 'https://github.com/AndreVerasFernandes/Order-API'
      },
      {
        name: 'Tomografo',
        desc: 'Academic project focused on data processing and analysis in notebook-based workflows.',
        stack: ['Python', 'Jupyter Notebook'],
        link: 'https://github.com/AndreVerasFernandes/Tomografo'
      }
    ]
  }
};

const t = computed(() => i18n[language.value]);
const skills = computed(() => skillMap[activeSkill.value]);

function getSkillIcon(skill) {
  return skillIcons[skill] || genericSkillIcon;
}

function applyTheme() {
  document.documentElement.classList.toggle('dark', theme.value === 'dark');
  localStorage.setItem('theme', theme.value);
}

function toggleTheme() {
  theme.value = theme.value === 'dark' ? 'light' : 'dark';
  applyTheme();
}

function toggleLanguage() {
  language.value = language.value === 'pt' ? 'en' : 'pt';
  localStorage.setItem('language', language.value);
}

onMounted(() => {
  const savedLanguage = localStorage.getItem('language');
  const savedTheme = localStorage.getItem('theme');

  if (savedLanguage === 'pt' || savedLanguage === 'en') {
    language.value = savedLanguage;
  }

  if (savedTheme === 'dark' || savedTheme === 'light') {
    theme.value = savedTheme;
  }

  applyTheme();

  const items = document.querySelectorAll('[data-reveal]');
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
          observer.unobserve(entry.target);
        }
      });
    },
    { threshold: 0.12 }
  );

  items.forEach((item) => observer.observe(item));
});
</script>

<template>
  <div class="page-shell">
    <div class="atmosphere" aria-hidden="true"></div>

    <main class="content">
      <section id="home" class="hero" data-reveal>
        <div>
          <div class="utility-bar">
            <button class="utility-btn" @click="toggleTheme">
              {{ t.utilityTheme }}: {{ theme === 'dark' ? 'Dark' : 'Light' }}
            </button>
            <button class="utility-btn" @click="toggleLanguage">
              {{ t.utilityLang }}: {{ language.toUpperCase() }}
            </button>
          </div>

          <p class="eyebrow">{{ t.heroEyebrow }}</p>
          <h1>{{ t.heroTitle }}</h1>
          <p class="lead">{{ t.heroLead }}</p>
          <div class="hero-links">
            <a class="inline-link" href="#projects">{{ t.heroCta }}</a>
          </div>
          
          <div class="social-links-hero">
            <a href="https://github.com/AndreVerasFernandes" target="_blank" rel="noopener noreferrer" class="social-link-hero" title="GitHub">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v 3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
              </svg>
            </a>
            <a href="https://www.linkedin.com/in/andre-veras-fernandes/" target="_blank" rel="noopener noreferrer" class="social-link-hero" title="LinkedIn">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.475-2.236-1.986-2.236-1.081 0-1.722.722-2.004 1.418-.103.249-.129.597-.129.946v5.441h-3.554s.05-8.736 0-9.646h3.554v1.364c.425-.654 1.185-1.586 2.882-1.586 2.105 0 3.685 1.377 3.685 4.344v5.524zM5.337 9.433c-1.144 0-1.915-.758-1.915-1.707 0-.955.77-1.708 1.963-1.708 1.193 0 1.914.753 1.939 1.708 0 .949-.746 1.707-1.987 1.707zm1.582 11.019H3.656V9.806h3.263v10.646zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.225 0z"/>
              </svg>
            </a>
          </div>
        </div>
      
      </section>

      <section id="about" class="block" data-reveal>
        <h2>{{ t.aboutTitle }}</h2>
        <p>{{ t.aboutText }}</p>
      </section>

      <section id="work" class="block" data-reveal>
        <h2>{{ t.workTitle }}</h2>
        <article v-for="job in t.work" :key="job.company" class="job-card">
          <header>
            <h3>{{ job.company }}</h3>
            <span>{{ job.period }}</span>
          </header>
          <p class="role">{{ job.role }}</p>
          <p v-if="job.employerLine" class="meta-line">{{ job.employerLine }}</p>
          <p v-if="job.location" class="meta-line">{{ job.location }}</p>
          <p v-if="job.summary">{{ job.summary }}</p>
          <ul>
            <li v-for="bullet in job.bullets" :key="bullet">{{ bullet }}</li>
          </ul>
        </article>
      </section>

      <section id="education" class="block" data-reveal>
        <h2>{{ t.educationTitle }}</h2>
        <article v-for="edu in t.education" :key="edu.institution" class="edu-card">
          <header>
            <h3>{{ edu.institution }}</h3>
            <span v-if="edu.period">{{ edu.period }}</span>
          </header>
          <p>{{ edu.degree }}</p>
        </article>
      </section>

      <section id="projects" class="block" data-reveal>
        <h2>{{ t.projectsTitle }}</h2>
        <div class="project-grid">
          <article v-for="project in t.projects" :key="project.name" class="project-card">
            <h3>{{ project.name }}</h3>
            <p>{{ project.desc }}</p>
            <div class="tags">
              <span v-for="tech in project.stack" :key="tech">{{ tech }}</span>
            </div>
            <a :href="project.link" class="project-link" target="_blank" rel="noopener noreferrer">
              {{ t.projectsCta }}
            </a>
          </article>
        </div>
      </section>

      <section id="skills" class="block" data-reveal>
        <h2>{{ t.skillsTitle }}</h2>
        <div class="skill-tabs">
          <button
            v-for="tab in skillTabs"
            :key="tab"
            :class="{ active: activeSkill === tab }"
            @click="activeSkill = tab"
          >
            {{ t.tabLabels[tab] }}
          </button>
        </div>
        <div class="skill-grid">
          <div v-for="skill in skills" :key="skill" class="skill-chip">
            <div class="skill-figure">
              <img :src="getSkillIcon(skill)" :alt="skill" loading="lazy" />
            </div>
            <span>{{ skill }}</span>
          </div>
        </div>
      </section>

      <section id="contact" class="block contact" data-reveal>
        <h2>{{ t.contactTitle }}</h2>
        <p>
          {{ t.contactText }}
          <a href="mailto:duverasusa@gmail.com">duverasusa@gmail.com</a>
        </p>
        
        <div class="social-links">
          <a href="https://github.com/AndreVerasFernandes" target="_blank" rel="noopener noreferrer" class="social-link" title="GitHub">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v 3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
            </svg>
          </a>
          <a href="https://www.linkedin.com/in/andre-veras-fernandes/" target="_blank" rel="noopener noreferrer" class="social-link" title="LinkedIn">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
              <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.475-2.236-1.986-2.236-1.081 0-1.722.722-2.004 1.418-.103.249-.129.597-.129.946v5.441h-3.554s.05-8.736 0-9.646h3.554v1.364c.425-.654 1.185-1.586 2.882-1.586 2.105 0 3.685 1.377 3.685 4.344v5.524zM5.337 9.433c-1.144 0-1.915-.758-1.915-1.707 0-.955.77-1.708 1.963-1.708 1.193 0 1.914.753 1.939 1.708 0 .949-.746 1.707-1.987 1.707zm1.582 11.019H3.656V9.806h3.263v10.646zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.225 0z"/>
            </svg>
          </a>
        </div>

        <form @submit.prevent>
          <input type="email" :placeholder="t.emailPlaceholder" required />
          <textarea :placeholder="t.messagePlaceholder" required></textarea>
          <button type="submit">{{ t.send }}</button>
        </form>
      </section>
    </main>

    <nav class="dock" aria-label="Quick links">
      <a href="#home">{{ t.nav.home }}</a>
      <a href="#about">{{ t.nav.about }}</a>
      <a href="#work">{{ t.nav.work }}</a>
      <a href="#education">{{ t.educationTitle }}</a>
      <a href="#projects">{{ t.nav.projects }}</a>
      <a href="#skills">{{ t.skillsTitle }}</a>
      <a href="#contact">{{ t.nav.contact }}</a>
    </nav>
  </div>
</template>
