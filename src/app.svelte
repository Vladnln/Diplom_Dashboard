<script>
  import Router, { link, location } from 'svelte-spa-router';
  import DashboardPage from './Pages/DashboardPage.svelte';
  import EventsPage from './Pages/EventsPage.svelte';
  import FilesPage from './Pages/FilesPage.svelte';
  import NotFoundPage from './Pages/NotFoundPage.svelte';

  const routes = {
    '/': DashboardPage,
    '/events': EventsPage,
    '/files': FilesPage,
    '*': NotFoundPage,
  };

  const navItems = [
    { path: '/', label: 'Главная', marker: 'ГЛ' },
    { path: '/events', label: 'События', marker: 'СБ' },
    { path: '/files', label: 'Файлы', marker: 'ФЛ' },
  ];

  const todayLabel = new Intl.DateTimeFormat('ru-RU', {
    weekday: 'long',
    month: 'short',
    day: 'numeric',
  }).format(new Date());

  $: currentPath = (($location ?? '/').split('?')[0].replace(/\/+$/, '')) || '/';
</script>

<div class="workspace-bg">
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>

  <div class="shell">
    <aside class="sidebar panel">
      <div class="brand">
        <div class="brand-mark">D</div>
        <div>
          <p class="brand-title">Диплом Space</p>
          <p class="brand-subtitle">Панель кафедры</p>
        </div>
      </div>

      <nav class="menu" aria-label="Главная навигация">
        {#each navItems as item}
          <a
            use:link
            href={item.path}
            class="menu-link"
            class:active={currentPath === item.path}
            aria-current={currentPath === item.path ? 'page' : undefined}
          >
            <span>{item.marker}</span>
            {item.label}
          </a>
        {/each}
      </nav>

      <!-- <div class="sidebar-card">
        <p class="card-caption">Дипломный спринт</p>
        <p class="card-title">12 заявок за неделю</p>
        <button type="button">Открыть таймлайн</button>
      </div> -->
    </aside>

    <section class="content">
      <header class="topbar panel">
        <label class="searchbox" for="search">
          <svg viewBox="0 0 24 24" aria-hidden="true">
            <path
              d="M10.5 3.75a6.75 6.75 0 1 0 4.26 11.99l3.75 3.76a.75.75 0 1 0 1.06-1.06l-3.76-3.75a6.75 6.75 0 0 0-5.31-10.94Zm0 1.5a5.25 5.25 0 1 1 0 10.5a5.25 5.25 0 0 1 0-10.5Z"
            />
          </svg>
          <input id="search" type="search" placeholder="Поиск проектов, студентов, задач..." />
        </label>

        <div class="top-actions">
          <p class="today">{todayLabel}</p>
          <button type="button" class="ghost-btn">Экспорт</button>
          <button type="button" class="pill-btn">Добавить проект</button>
        </div>
      </header>

      <div class="route-panel panel">
        <Router {routes} />
      </div>
    </section>
  </div>
</div>

<style>
  .workspace-bg {
    position: relative;
    min-height: 100vh;
    padding: clamp(1rem, 3vw, 2rem);
    overflow: hidden;
  }

  .orb {
    position: absolute;
    border-radius: 999px;
    filter: blur(8px);
    pointer-events: none;
    z-index: 0;
  }

  .orb-1 {
    width: 380px;
    height: 380px;
    left: -100px;
    top: -120px;
    background: radial-gradient(circle, rgba(36, 126, 97, 0.22) 0%, rgba(36, 126, 97, 0) 70%);
  }

  .orb-2 {
    width: 420px;
    height: 420px;
    right: -160px;
    top: 30%;
    background: radial-gradient(circle, rgba(244, 181, 87, 0.22) 0%, rgba(244, 181, 87, 0) 70%);
  }

  .orb-3 {
    width: 280px;
    height: 280px;
    left: 40%;
    bottom: -120px;
    background: radial-gradient(circle, rgba(89, 157, 255, 0.14) 0%, rgba(89, 157, 255, 0) 70%);
  }

  .shell {
    position: relative;
    z-index: 2;
    max-width: 1400px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 250px 1fr;
    gap: 1rem;
  }

  .panel {
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 24px;
    box-shadow: var(--shadow);
  }

  .sidebar {
    display: flex;
    flex-direction: column;
    gap: 1.8rem;
    padding: 1.4rem;
  }

  .brand {
    display: flex;
    align-items: center;
    gap: 0.8rem;
  }

  .brand-mark {
    display: grid;
    place-items: center;
    width: 2.25rem;
    height: 2.25rem;
    border-radius: 14px;
    background: linear-gradient(150deg, var(--accent) 0%, #41b37f 100%);
    color: #fff;
    font-family: 'Sora', sans-serif;
    font-weight: 700;
  }

  .brand-title {
    margin: 0;
    font-family: 'Sora', sans-serif;
    font-size: 1rem;
    font-weight: 600;
  }

  .brand-subtitle {
    margin: 0.2rem 0 0;
    color: var(--text-dim);
    font-size: 0.76rem;
  }

  .menu {
    display: flex;
    flex-direction: column;
    gap: 0.38rem;
  }

  .menu-link {
    display: flex;
    align-items: center;
    gap: 0.65rem;
    padding: 0.7rem 0.8rem;
    border-radius: 12px;
    color: var(--text-soft);
    font-weight: 600;
    transition: background 0.2s ease, color 0.2s ease, transform 0.2s ease;
  }

  .menu-link span {
    display: grid;
    place-items: center;
    min-width: 2rem;
    height: 2rem;
    border-radius: 10px;
    background: #eef2f0;
    color: #406053;
    font-size: 0.68rem;
    letter-spacing: 0.05em;
    font-family: 'Sora', sans-serif;
    font-weight: 600;
  }

  .menu-link:hover {
    background: #f0f7f4;
    color: var(--text-main);
    transform: translateX(2px);
  }

  .menu-link.active {
    background: linear-gradient(135deg, #e9f8f1 0%, #f6fbf8 100%);
    color: var(--text-main);
    box-shadow: inset 0 0 0 1px #d0ecdf;
  }

  .menu-link.active span {
    background: linear-gradient(150deg, var(--accent) 0%, #46b985 100%);
    color: #fff;
  }

  /* .sidebar-card {
    margin-top: auto;
    padding: 1rem;
    border-radius: 18px;
    background: linear-gradient(145deg, #173d32 0%, #246451 50%, #1f5445 100%);
    color: #e8fbf3;
  }

  .card-caption {
    margin: 0;
    font-size: 0.72rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    opacity: 0.76;
  }

  .card-title {
    margin: 0.45rem 0 1rem;
    font-size: 1rem;
    font-weight: 700;
  }

  .sidebar-card button {
    width: 100%;
    border: none;
    border-radius: 999px;
    padding: 0.6rem 0.9rem;
    font-weight: 700;
    color: #0f2f26;
    background: #d5f2e4;
    cursor: pointer;
  } */

  .content {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    min-width: 0;
  }

  .topbar {
    display: flex;
    align-items: center;
    gap: 1rem;
    justify-content: space-between;
    padding: 1rem 1.25rem;
  }

  .searchbox {
    display: flex;
    align-items: center;
    gap: 0.55rem;
    min-width: 0;
    flex: 1;
    max-width: 490px;
    border-radius: 13px;
    border: 1px solid #deebe4;
    background: #f8fbf9;
    padding: 0.48rem 0.7rem;
  }

  .searchbox svg {
    width: 1.1rem;
    height: 1.1rem;
    fill: #7c9488;
    flex-shrink: 0;
  }

  .searchbox input {
    width: 100%;
    border: none;
    background: transparent;
    color: var(--text-main);
    outline: none;
  }

  .top-actions {
    display: flex;
    align-items: center;
    gap: 0.65rem;
  }

  .today {
    margin: 0;
    color: var(--text-dim);
    font-size: 0.8rem;
    font-weight: 600;
  }

  .ghost-btn,
  .pill-btn {
    border-radius: 999px;
    padding: 0.58rem 1rem;
    font-size: 0.82rem;
    font-weight: 700;
    cursor: pointer;
    border: 1px solid transparent;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }

  .ghost-btn {
    background: #f3f8f6;
    border-color: #dce8e1;
    color: #305045;
  }

  .pill-btn {
    background: linear-gradient(140deg, var(--accent) 0%, #3fb17e 100%);
    color: #fff;
    box-shadow: 0 10px 16px rgba(23, 102, 75, 0.22);
  }

  .ghost-btn:hover,
  .pill-btn:hover {
    transform: translateY(-1px);
  }

  .route-panel {
    min-height: calc(100vh - 6.5rem);
    padding: clamp(1rem, 2.2vw, 1.5rem);
    overflow: hidden;
  }

  @media (max-width: 1200px) {
    .top-actions .today {
      display: none;
    }
  }

  @media (max-width: 980px) {
    .shell {
      grid-template-columns: 1fr;
    }

    .sidebar {
      gap: 1rem;
    }

    .menu {
      flex-direction: row;
      flex-wrap: wrap;
    }

    .menu-link {
      flex: 1 1 30%;
      min-width: 150px;
    }

    /* .sidebar-card {
      margin-top: 0.2rem;
    } */

    .topbar {
      flex-wrap: wrap;
    }
  }

  @media (max-width: 640px) {
    .workspace-bg {
      padding: 0.6rem;
    }

    .sidebar,
    .topbar,
    .route-panel {
      border-radius: 18px;
    }

    .menu-link {
      min-width: 0;
      flex: 1 1 100%;
    }

    .top-actions {
      width: 100%;
      justify-content: flex-end;
      flex-wrap: wrap;
    }
  }
</style>
