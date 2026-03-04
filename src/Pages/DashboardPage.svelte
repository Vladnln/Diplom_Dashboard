<script>
  const projectStats = [
    { title: 'Всего проектов', value: 24, meta: '+8% к прошлому месяцу' },
    { title: 'Завершено', value: 10, meta: '+2 закрыто за неделю' },
    { title: 'В работе', value: 12, meta: '4 близко к этапу сдачи' },
    { title: 'На проверке', value: 2, meta: 'Ожидают комиссию' },
  ];

  const weeklyLoad = [52, 78, 63, 86, 57, 68, 40];
  const weekDays = ['Вс', 'Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб'];

  const teamMembers = [
    {
      name: 'Александра Боирсова',
      task: 'Репозиторий проекта в GitHub',
      statusLabel: 'Завершено',
      statusClass: 'completed',
    },
    {
      name: 'Эрик Агаджанян',
      task: 'Интеграция модуля',
      statusLabel: 'В процессе',
      statusClass: 'in-progress',
    },
    {
      name: 'Альберт Измаилов',
      task: 'Поиск и фильтрация информации',
      statusLabel: 'В ожидании',
      statusClass: 'pending',
    },
    {
      name: 'Давид Лавров',
      task: 'Заполнение тех задания',
      statusLabel: 'В процессе',
      statusClass: 'in-progress',
    },
  ];

  const initiatives = [
    'Собрать макет панели',
    
  ];

  const progress = 41;
</script>

<section class="page dashboard">
  <header class="page-head">
    <div>
      <p class="eyebrow">Учебные процессы</p>
      <h1>Панель кафедры</h1>
      <p class="sub">
        Планируйте, приоритизируйте и контролируйте дипломные потоки кафедры в одном окне.
      </p>
    </div>
  </header>

  <section class="stats-grid">
    {#each projectStats as stat, index}
      <article class="card stat-card {index === 0 ? 'accent' : ''}">
        <p>{stat.title}</p>
        <h2>{stat.value}</h2>
        <small>{stat.meta}</small>
      </article>
    {/each}
  </section>

  <section class="dashboard-grid">
    <article class="card analytics">
      <div class="card-head">
        <h3>Аналитика проектов</h3>
      </div>
      <div class="bars">
        {#each weeklyLoad as value, index}
          <div class="bar-wrap">
            <span class="bar" style={`--height:${value}%`}></span>
            <small>{weekDays[index]}</small>
          </div>
        {/each}
      </div>
    </article>

    <article class="card reminders">
      <div class="card-head">
        <h3>Напоминание</h3>
      </div>
      <p class="meeting-title">Встреча с научными руководителями</p>
      <p class="meeting-time">10:00 - 16:00</p>
      <button type="button">Начать встречу</button>
    </article>

    <article class="card project-list">
      <div class="card-head">
        <h3>Очередь задач</h3>
      </div>
      <ul>
        {#each initiatives as item}
          <li>
            <span class="dot"></span>
            {item}
          </li>
        {/each}
      </ul>
    </article>

    <article class="card collaborators">
      <div class="card-head">
        <h3>Командная работа</h3>
        <button type="button" class="small">+ Добавить</button>
      </div>
      <ul>
        {#each teamMembers as member}
          <li>
            <div class="avatar">{member.name[0]}</div>
            <div class="member-info">
              <p>{member.name}</p>
              <small>{member.task}</small>
            </div>
            <span class="status {member.statusClass}">{member.statusLabel}</span>
          </li>
        {/each}
      </ul>
    </article>

    <article class="card progress-card">
      <div class="card-head">
        <h3>Прогресс проекта</h3>
      </div>
      <div class="ring" style={`--progress:${progress}%`}>
        <div class="ring-core">
          <strong>{progress}%</strong>
          <span>выполнено</span>
        </div>
      </div>
      <div class="legend">
        <span><i class="ok"></i>Завершено</span>
        <span><i class="work"></i>В процессе</span>
        <span><i class="pending"></i>Ожидает</span>
      </div>
    </article>

    <article class="card tracker">
      <p class="eyebrow">Трекер времени</p>
      <h3>01:24:08</h3>
      <div class="tracker-actions">
        <button type="button" class="pause">Пауза</button>
        <button type="button" class="stop">Стоп</button>
      </div>
    </article>
  </section>
</section>

<style>
  .stats-grid {
    display: grid;
    gap: 0.75rem;
    grid-template-columns: repeat(4, minmax(0, 1fr));
  }

  .stat-card {
    padding: 1rem;
  }

  .stat-card p {
    color: var(--text-soft);
    font-weight: 600;
  }

  .stat-card h2 {
    margin-top: 0.35rem;
    font-size: clamp(1.65rem, 4vw, 2.2rem);
  }

  .stat-card small {
    color: var(--text-dim);
    font-weight: 600;
  }

  .stat-card.accent {
    background: linear-gradient(140deg, #197c59 0%, #2da176 100%);
    color: #f2fff8;
    border-color: #1e8864;
    box-shadow: 0 14px 26px rgba(33, 117, 86, 0.24);
  }

  .stat-card.accent p,
  .stat-card.accent small {
    color: rgba(242, 255, 248, 0.9);
  }

  .dashboard-grid {
    display: grid;
    gap: 0.75rem;
    grid-template-columns: repeat(4, minmax(0, 1fr));
  }

  .analytics {
    grid-column: span 2;
    padding: 1rem;
  }

  .card-head {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 0.8rem;
  }

  .bars {
    display: grid;
    grid-template-columns: repeat(7, minmax(0, 1fr));
    gap: 0.65rem;
    min-height: 180px;
    align-items: end;
  }

  .bar-wrap {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.42rem;
  }

  .bar {
    width: 100%;
    min-height: 1.2rem;
    height: var(--height);
    border-radius: 999px;
    background: repeating-linear-gradient(
      -45deg,
      #d7e7df 0px,
      #d7e7df 4px,
      #edf5f1 4px,
      #edf5f1 9px
    );
  }

  .bar-wrap:nth-child(2n) .bar {
    background: linear-gradient(180deg, #56c39a 0%, #228860 100%);
  }

  .bar-wrap:nth-child(4) .bar {
    background: linear-gradient(180deg, #1e724f 0%, #0f5b3d 100%);
  }

  .bar-wrap small {
    font-size: 0.72rem;
    font-weight: 700;
    color: var(--text-dim);
  }

  .reminders {
    padding: 1rem;
  }

  .meeting-title {
    font-size: 1.4rem;
    font-weight: 700;
    font-family: 'Sora', sans-serif;
    line-height: 1.2;
  }

  .meeting-time {
    margin-top: 0.32rem;
    color: var(--text-dim);
  }

  .reminders button {
    margin-top: 1rem;
    width: 100%;
    border: none;
    padding: 0.7rem 0.9rem;
    border-radius: 999px;
    background: linear-gradient(130deg, #1f8e67 0%, #3aae80 100%);
    color: #fff;
    font-weight: 700;
    cursor: pointer;
  }

  .project-list {
    padding: 1rem;
  }

  .project-list ul {
    margin: 0;
    padding: 0;
    list-style: none;
    display: grid;
    gap: 0.6rem;
  }

  .project-list li {
    display: flex;
    align-items: center;
    gap: 0.55rem;
    color: var(--text-soft);
    font-weight: 600;
  }

  .dot {
    width: 0.5rem;
    height: 0.5rem;
    border-radius: 99px;
    background: linear-gradient(160deg, #289668 0%, #5cc9a1 100%);
    flex-shrink: 0;
  }

  .collaborators {
    grid-column: span 2;
    padding: 1rem;
  }

  .small {
    border: 1px solid #d7e5dd;
    border-radius: 999px;
    background: #f8fbf9;
    color: var(--text-soft);
    font-weight: 700;
    font-size: 0.74rem;
    padding: 0.42rem 0.76rem;
    cursor: pointer;
  }

  .collaborators ul {
    margin: 0;
    padding: 0;
    list-style: none;
    display: grid;
    gap: 0.65rem;
  }

  .collaborators li {
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: 0.65rem;
  }

  .avatar {
    width: 2rem;
    height: 2rem;
    border-radius: 999px;
    display: grid;
    place-items: center;
    background: linear-gradient(140deg, #ffe7bb 0%, #f5c772 100%);
    color: #5f3d0d;
    font-weight: 700;
    font-family: 'Sora', sans-serif;
  }

  .member-info p {
    font-weight: 700;
  }

  .member-info small {
    color: var(--text-dim);
  }

  .status {
    border-radius: 999px;
    padding: 0.24rem 0.55rem;
    font-size: 0.67rem;
    font-weight: 700;
  }

  .status.completed {
    color: #146347;
    background: #dcf5ea;
  }

  .status.in-progress {
    color: #835307;
    background: #fbeecb;
  }

  .status.pending {
    color: #7d3453;
    background: #f8dce8;
  }

  .progress-card {
    padding: 1rem;
    display: flex;
    flex-direction: column;
    gap: 0.7rem;
  }

  .ring {
    --progress: 0%;
    width: min(100%, 240px);
    aspect-ratio: 1 / 1;
    margin: 0 auto;
    border-radius: 50%;
    display: grid;
    place-items: center;
    background: conic-gradient(#19845f var(--progress), #d9e8e1 var(--progress) 100%);
  }

  .ring-core {
    width: 72%;
    height: 72%;
    border-radius: 50%;
    background: #fff;
    display: grid;
    place-items: center;
    text-align: center;
    box-shadow: inset 0 0 0 1px #e0e9e4;
  }

  .ring-core strong {
    font-size: 2rem;
    font-family: 'Sora', sans-serif;
  }

  .ring-core span {
    margin-top: -0.2rem;
    color: var(--text-dim);
    font-size: 0.75rem;
    font-weight: 700;
  }

  .legend {
    display: flex;
    justify-content: center;
    gap: 0.65rem;
    flex-wrap: wrap;
  }

  .legend span {
    display: inline-flex;
    align-items: center;
    gap: 0.35rem;
    font-size: 0.74rem;
    color: var(--text-dim);
    font-weight: 700;
  }

  .legend i {
    width: 0.5rem;
    height: 0.5rem;
    border-radius: 50%;
    display: inline-block;
  }

  .legend .ok {
    background: #1a8a63;
  }

  .legend .work {
    background: #5db895;
  }

  .legend .pending {
    background: #d5e1db;
  }

  .tracker {
    padding: 1rem;
    color: #e9fff5;
    background:
      radial-gradient(circle at 75% 20%, rgba(120, 255, 196, 0.2), transparent 50%),
      linear-gradient(140deg, #0d291f 0%, #114636 60%, #1f6d53 100%);
    border-color: #1b5a45;
  }

  .tracker h3 {
    margin-top: 0.4rem;
    font-size: 2rem;
  }

  .tracker-actions {
    display: flex;
    gap: 0.55rem;
    margin-top: 1rem;
  }

  .tracker-actions button {
    border: none;
    padding: 0.5rem 0.85rem;
    border-radius: 999px;
    font-size: 0.75rem;
    font-weight: 700;
    cursor: pointer;
  }

  .pause {
    background: #effcf5;
    color: #14563f;
  }

  .stop {
    background: #ffe2de;
    color: #8b251b;
  }

  @media (max-width: 1120px) {
    .stats-grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }

    .dashboard-grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }
  }

  @media (max-width: 760px) {
    .stats-grid,
    .dashboard-grid {
      grid-template-columns: 1fr;
    }

    .analytics,
    .collaborators {
      grid-column: auto;
    }
  }
</style>
