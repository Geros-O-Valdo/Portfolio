<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
import TechCard from "./components/TechCard.vue";
</script>

<script>
export default {
  data() {
    return {
      isDarkMode: document.documentElement.classList.contains("dark"),
      isConfigOpen: false,
      currentLang: "pt",
    };
  },
  methods: {
    toggleTheme() {
      this.isDarkMode = !this.isDarkMode;
      localStorage.setItem("theme", this.isDarkMode ? "dark" : "light");
      this.updateTheme();
    },
    updateTheme() {
      if (this.isDarkMode) {
        document.documentElement.classList.add("dark");
      } else {
        document.documentElement.classList.remove("dark");
      }
    },
  },
};
</script>

<template>
  <!-- Header fixo no topo -->
  <header class="fixed top-0 right-0 p-4 flex items-center gap-2 group">
    <div class="relative">
      <!-- Ícone da Engrenagem (sempre visível e rotaciona no hover) -->
      <div
        class="cursor-pointer transition-transform duration-500 transform group-hover:rotate-180 px-2"
      >
        <svg
          class="w-8 h-8 text-current"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="1.5"
            d="M21 13v-2a1 1 0 0 0-1-1h-.757l-.707-1.707.535-.536a1 1 0 0 0 0-1.414l-1.414-1.414a1 1 0 0 0-1.414 0l-.536.535L14 4.757V4a1 1 0 0 0-1-1h-2a1 1 0 0 0-1 1v.757l-1.707.707-.536-.535a1 1 0 0 0-1.414 0L4.929 6.343a1 1 0 0 0 0 1.414l.536.536L4.757 10H4a1 1 0 0 0-1 1v2a1 1 0 0 0 1 1h.757l.707 1.707-.535.536a1 1 0 0 0 0 1.414l1.414 1.414a1 1 0 0 0 1.414 0l.536-.535 1.707.707V20a1 1 0 0 0 1 1h2a1 1 0 0 0 1-1v-.757l1.707-.708.536.536a1 1 0 0 0 1.414 0l1.414-1.414a1 1 0 0 0 0-1.414l-.535-.536.707-1.707H20a1 1 0 0 0 1-1Z"
          />
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="1.5"
            d="M12 15a3 3 0 1 0 0-6 3 3 0 0 0 0 6Z"
          />
        </svg>
      </div>

      <!-- Container de Toggles (slide in/out) -->
      <div class="absolute top-0 right-full flex flex-row items-center space-x-2">
        <!-- Toggle do Tema -->
        <div
          @click="toggleTheme"
          class="transition-all duration-300 transform translate-x-full opacity-0 pointer-events-none group-hover:translate-x-0 group-hover:opacity-100 group-hover:pointer-events-auto"
        >
          <div
            :class="[
              'border-2 rounded-full p-1 h-8 w-20 flex items-center transition-all duration-300 cursor-pointer',
              isDarkMode ? 'bg-gray-800' : 'bg-white',
            ]"
          >
            <div
              class="size-6 transition-transform duration-300 transform"
              :class="isDarkMode ? 'translate-x-11' : 'translate-x-0'"
            >
              <svg
                v-if="isDarkMode"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                class="w-6 h-6 text-white"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="1"
                  d="M21.752 15.002A9.72 9.72 0 0 1 18 15.75c-5.385 0-9.75-4.365-9.75-9.75 0-1.33.266-2.597.748-3.752A9.753 9.753 0 0 0 3 11.25C3 16.635 7.365 21 12.75 21a9.753 9.753 0 0 0 9.002-5.998Z"
                />
              </svg>
              <svg
                v-else
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6 text-black"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M12 5V3m0 18v-2M7.05 7.05 5.636 5.636m12.728 12.728L16.95 16.95M5 12H3m18 0h-2M7.05 16.95l-1.414 1.414M18.364 5.636 16.95 7.05M16 12a4 4 0 1 1-8 0 4 4 0 0 1 8 0Z"
                />
              </svg>
            </div>
          </div>
        </div>

        <!-- Select de idioma (com padding interno) -->
        <div
          :class="[
            'relative flex items-center h-8 border-2 rounded-full transition-all duration-300 cursor-pointer',
            isDarkMode ? 'bg-gray-800 border-white' : 'bg-white border-black',
            'transform translate-x-full opacity-0 pointer-events-none',
            'group-hover:translate-x-0 group-hover:opacity-100 group-hover:pointer-events-auto',
          ]"
        >
          <select
            ref="sel"
            v-model="currentLang"
            @change="changeLanguage"
            :class="[
              'appearance-none w-32 h-full text-sm outline-none bg-transparent pl-3 pr-2',
              isDarkMode ? 'text-white' : 'text-black',
            ]"
          >
            <option class="text-black pl-2" value="pt">PT – Português</option>
            <option class="text-black pl-2" value="en">EN – English</option>
            <option class="text-black pl-2" value="es">ES – Español</option>
          </select>
          <svg
            class="w-4 h-4 absolute right-2 pointer-events-none"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            :class="isDarkMode ? 'text-white' : 'text-black'"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M19 9l-7 7-7-7"
            />
          </svg>
        </div>
      </div>
    </div>
  </header>
  <main class="">
    <nav
      class="fixed left-0 top-0 h-screen w-32 p-4 border-r-2 border-gray-200 flex flex-col justify-center items-center"
    >
      <ul class="flex flex-col items-center justify-center h-full space-y-2">
        <li class="group relative flex flex-col items-center">
          <a href="#" class="block py-2">
            <svg
              class="w-8 h-8"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="1"
                d="m4 12 8-8 8 8M6 10.5V19a1 1 0 0 0 1 1h3v-3a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1v3h3a1 1 0 0 0 1-1v-8.5"
              />
            </svg>
          </a>
          <span
            class="absolute left-12 opacity-0 group-hover:opacity-100 transition-opacity bg-gray-800 text-white text-sm rounded-md px-2 py-1"
            >Home</span
          >
        </li>
        <li class="text-center">•</li>
        <li class="group relative flex flex-col items-center">
          <a href="#" class="block py-2">
            <svg
              class="w-8 h-8"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="1"
                d="M15 9h3m-3 3h3m-3 3h3m-6 1c-.306-.613-.933-1-1.618-1H7.618c-.685 0-1.312.387-1.618 1M4 5h16a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1Zm7 5a2 2 0 1 1-4 0 2 2 0 0 1 4 0Z"
              />
            </svg>
          </a>
          <span
            class="absolute left-12 opacity-0 group-hover:opacity-100 transition-opacity bg-gray-800 text-white text-sm rounded-md px-2 py-1"
            >Experiência</span
          >
        </li>
        <li class="text-center">•</li>
        <li class="group relative flex flex-col items-center">
          <a href="#" class="block py-2">
            <svg
              class="w-8 h-8"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="1"
                d="M13.5 8H4m0-2v13a1 1 0 0 0 1 1h14a1 1 0 0 0 1-1V9a1 1 0 0 0-1-1h-5.032a1 1 0 0 1-.768-.36l-1.9-2.28a1 1 0 0 0-.768-.36H5a1 1 0 0 0-1 1Z"
              />
            </svg>
          </a>
          <span
            class="absolute left-12 opacity-0 group-hover:opacity-100 transition-opacity bg-gray-800 text-white text-sm rounded-md px-2 py-1"
            >Projetos</span
          >
        </li>
        <li class="text-center">•</li>
        <li class="group relative flex flex-col items-center">
          <a href="#" class="block py-2">
            <svg
              class="w-8 h-8"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-width="1"
                d="m3.5 5.5 7.893 6.036a1 1 0 0 0 1.214 0L20.5 5.5M4 19h16a1 1 0 0 0 1-1V6a1 1 0 0 0-1-1H4a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1Z"
              />
            </svg>
          </a>
          <span
            class="absolute left-12 opacity-0 group-hover:opacity-100 transition-opacity bg-gray-800 text-white text-sm rounded-md px-2 py-1"
            >Contato</span
          >
        </li>
      </ul>
    </nav>
    <div class="ml-34 pl-20 pr-14 mt-22">
      <h1 class="text-7xl">Gabriel Kutner Novotni</h1>
      <h2 class="text-4xl mt-1 ml-2">Full Stack Developer</h2>
      <div class="my-6 mt-12 flex space-x-4">
        <div class="text-xl flex-1 space-y-4">
          <!-- <p>Estou atualmente cursando o 5° ano de Engenharia de Software na UEPG (Universidade Estadual de Ponta Grossa).</p> -->
          <p>
            Sou um desenvolvedor dedicado à transformar ideias em soluções reais. Buscando
            constantemente evoluir, aprender novas tecnologias e enfrentar desafios com
            criatividade e dedicação.
          </p>
          <p>
            Tenho experiência sólida no desenvolvimento web, criação de APIs, modelagem de
            bancos de dados e integração de sistemas. Gosto de aprender, experimentar
            novas tecnologias e aplicar metodologias ágeis para garantir processos mais
            organizados e produtivos.
            <!--e estou sempre aberto a explorar novas ferramentas e metodologias que contribuam para
            a qualidade e eficiência do que entrego. -->
          </p>
          <p>
            Mais do que escrever código, acredito em desenvolver softwares e prover um
            serviço que se comunica com os todos os envolvidos.
          </p>
        </div>

        <!-- Ajustando a posição da imagem -->
        <div
          class="bg-gray-200 w-[450px] h-[450px] rounded-full overflow-hidden flex items-center justify-center shadow-lg border-2"
          style="margin-top: -100px"
        >
          <img
            src="/images/jan_matejko_stac584czyk.webp"
            alt="Minha Imagem"
            class="w-full h-full object-cover"
          />
        </div>
      </div>

      <div class="mt-32">
        <h1 class="text-4xl mb-6 text-center">Tecnologias Principais</h1>
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
          <TechCard
            icon="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/vuejs/vuejs-original.svg"
            title="Vue.js"
            subtitle="Framework FrontEnd"
          />
          <TechCard
            icon="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tailwindcss/tailwindcss-original.svg"
            title="Tailwind CSS"
            subtitle="Framework de Estilização"
          />
          <TechCard
            icon="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/laravel/laravel-original.svg"
            title="Laravel"
            subtitle="Framework Backend PHP"
          />
          <TechCard
            icon="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mysql/mysql-original.svg"
            title="MySQL"
            subtitle="Banco de Dados Relacional"
          />
          <TechCard
            icon="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/python/python-original.svg"
            title="Python"
            subtitle="Linguagem Multiuso"
            bgColor="bg-gray-900"
          />
          <TechCard
            icon="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/github/github-original.svg"
            title="GitHub"
            subtitle="Ferramenta de Versionamento"
            bgColor=""
          />
        </div>
      </div>

    <section class="mt-20">
  <h1 class="text-4xl font-extrabold text-center text-gray-900 dark:text-white mb-12">
    Histórico Técnico / Profissional
  </h1>

  <div class="flex flex-col gap-10 border-l-2 border-gray-300 dark:border-gray-600 pl-6">
    <!-- Emprego mais recente -->
    <div>
      <p class="text-xs text-gray-500 dark:text-gray-400 uppercase tracking-wide mb-1">2023 – Atual</p>
      <h3 class="text-2xl font-semibold text-gray-900 dark:text-white">
        Desenvolvedor Full Stack — Estágio na Prefeitura
      </h3>
      <p class="text-gray-700 dark:text-gray-300 mt-2 leading-relaxed">
        Desenvolvimento de sistemas internos com foco em Vue, Laravel e MySQL. Atuação em APIs REST e automação de processos internos.
      </p>
    </div>

    <!-- Formação acadêmica -->
    <div>
      <p class="text-xs text-gray-500 dark:text-gray-400 uppercase tracking-wide mb-1">Graduação</p>
      <h3 class="text-2xl font-semibold text-gray-900 dark:text-white">
        Engenharia de Software — UEPG
      </h3>
      <p class="text-gray-700 dark:text-gray-300 mt-2 leading-relaxed">
        Graduando em Engenharia de Software.
      </p>
    </div>
  </div>
</section>


      <div v-for="i in 10" class="mt-16">
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rem, voluptas unde?
        Exercitationem molestias voluptatibus omnis cumque tenetur at! Ut nam magnam
        ducimus nobis neque obcaecati maiores, ea earum blanditiis non.
      </div>
    </div>
  </main>
</template>

<style></style>
