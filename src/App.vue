<script setup lang="ts"></script>

<template>
  <div class="app">

    <!-- Cabeçalho -->
    <header class="header">
      <div class="logo">
        <h1>Meu Projeto</h1>
      </div>

      <nav class="nav">
        <a href="#inicio">Início</a>
        <a href="#sobre">Sobre</a>
        <a href="#projetos">Projetos</a>
        <a href="#contato">Contato</a>
      </nav>

      <button class="btn-menu">
        Menu
      </button>
    </header>


    <!-- Conteúdo principal -->
    <main>

      <!-- Seção inicial -->
      <section id="inicio" class="hero">

        <div class="hero-content">
          <span class="subtitle">Olá, seja bem-vindo!</span>

          <h2>
            Desenvolvedor
            <span>Web</span>
          </h2>

          <p>
            Este é o meu projeto desenvolvido utilizando Vue.js.
            Aqui posso apresentar meus conhecimentos, projetos e experiências.
          </p>

          <div class="hero-buttons">
            <button class="btn-primary">
              Conheça meu projeto
            </button>

            <button class="btn-secondary">
              Saiba mais
            </button>
          </div>
        </div>

        <div class="hero-image">
          <div class="image-placeholder">
            Imagem
          </div>
        </div>

      </section>


      <!-- Seção sobre -->
      <section id="sobre" class="about">

        <div class="section-title">
          <span>01</span>
          <h2>Sobre mim</h2>
        </div>

        <div class="about-content">

          <div class="about-image">
            <div class="image-placeholder">
              Foto
            </div>
          </div>

          <div class="about-text">
            <h3>Quem sou eu?</h3>

            <p>
              Aqui você pode escrever uma apresentação sobre você,
              seus estudos, experiências e objetivos profissionais.
            </p>

            <p>
              Também pode colocar informações sobre as tecnologias
              que você utiliza e os tipos de projetos que desenvolve.
            </p>

            <button class="btn-primary">
              Ver mais
            </button>
          </div>

        </div>

      </section>


      <!-- Tecnologias -->
      <section class="technologies">

        <div class="section-title">
          <span>02</span>
          <h2>Tecnologias</h2>
        </div>

        <div class="technology-grid">

          <div class="technology-card">
            <h3>HTML</h3>
            <p>Estrutura das aplicações web.</p>
          </div>

          <div class="technology-card">
            <h3>CSS</h3>
            <p>Estilização e responsividade.</p>
          </div>

          <div class="technology-card">
            <h3>JavaScript</h3>
            <p>Interatividade e lógica.</p>
          </div>

          <div class="technology-card">
            <h3>Vue.js</h3>
            <p>Desenvolvimento de interfaces.</p>
          </div>

          <div class="technology-card">
            <h3>Git</h3>
            <p>Controle de versão.</p>
          </div>

          <div class="technology-card">
            <h3>GitHub</h3>
            <p>Hospedagem dos projetos.</p>
          </div>

        </div>

      </section>


      <!-- Projetos -->
      <section id="projetos" class="projects">

        <div class="section-title">
          <span>03</span>
          <h2>Projetos</h2>
        </div>

        <div class="project-grid">

          <article class="project-card">

            <div class="project-image">
              Preview
            </div>

            <div class="project-content">
              <span class="project-category">
                Desenvolvimento Web
              </span>

              <h3>Projeto 01</h3>

              <p>
                Descrição do projeto desenvolvido.
              </p>

              <div class="project-technologies">
                <span>Vue</span>
                <span>CSS</span>
                <span>JavaScript</span>
              </div>

              <a href="#" class="project-link">
                Ver projeto →
              </a>
            </div>

          </article>


          <article class="project-card">

            <div class="project-image">
              Preview
            </div>

            <div class="project-content">
              <span class="project-category">
                Front-end
              </span>

              <h3>Projeto 02</h3>

              <p>
                Descrição do segundo projeto.
              </p>

              <div class="project-technologies">
                <span>HTML</span>
                <span>CSS</span>
                <span>JavaScript</span>
              </div>

              <a href="#" class="project-link">
                Ver projeto →
              </a>
            </div>

          </article>


          <article class="project-card">

            <div class="project-image">
              Preview
            </div>

            <div class="project-content">
              <span class="project-category">
                Aplicação
              </span>

              <h3>Projeto 03</h3>

              <p>
                Descrição do terceiro projeto.
              </p>

              <div class="project-technologies">
                <span>Vue</span>
                <span>API</span>
              </div>

              <a href="#" class="project-link">
                Ver projeto →
              </a>
            </div>

          </article>

        </div>

      </section>


      <!-- Contato -->
      <section id="contato" class="contact">

        <div class="section-title">
          <span>04</span>
          <h2>Entre em contato</h2>
        </div>

        <div class="contact-content">

          <div class="contact-info">
            <h3>Vamos conversar?</h3>

            <p>
              Se quiser entrar em contato comigo, utilize
              uma das opções abaixo.
            </p>

            <div class="contact-item">
              <strong>Email</strong>
              <span>seuemail@email.com</span>
            </div>

            <div class="contact-item">
              <strong>GitHub</strong>
              <span>github.com/seuusuario</span>
            </div>

            <div class="contact-item">
              <strong>LinkedIn</strong>
              <span>linkedin.com/in/seuusuario</span>
            </div>
          </div>


          <form class="contact-form">

            <div class="form-group">
              <label for="name">Nome</label>
              <input
                id="name"
                type="text"
                placeholder="Digite seu nome"
              />
            </div>

            <div class="form-group">
              <label for="email">Email</label>
              <input
                id="email"
                type="email"
                placeholder="Digite seu email"
              />
            </div>

            <div class="form-group">
              <label for="message">Mensagem</label>
              <textarea
                id="message"
                rows="6"
                placeholder="Digite sua mensagem"
              ></textarea>
            </div>

            <button type="submit" class="btn-primary">
              Enviar mensagem
            </button>

          </form>

        </div>

      </section>

    </main>


    <!-- Rodapé -->
    <footer class="footer">

      <p>
        © 2026 Meu Projeto. Todos os direitos reservados.
      </p>

      <div class="social-links">
        <a href="#">GitHub</a>
        <a href="#">LinkedIn</a>
        <a href="#">Instagram</a>
      </div>

    </footer>

  </div>
</template>

<script setup>
// Lógica do componente pode ser adicionada aqui
</script>


<style scoped>
<style scoped>
h1 {
  color: purple;
  font-size: 48px;
}
</style>
