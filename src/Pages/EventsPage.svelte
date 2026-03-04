<script>
  const todo = [
    {
      title: 'Запланировать прием эндокринолога',
      days: 15,
      comments: 6,
      priorityLabel: 'Высокий',
      priorityClass: 'high',
    },
    {
      title: 'Помочь DStudio с онбординг-кампанией',
      days: 15,
      comments: 23,
      priorityLabel: 'Средний',
      priorityClass: 'medium',
    },
  ];

  const inProgress = [
    {
      title: 'Спланировать мероприятие кафедры',
      days: 15,
      comments: 7,
      priorityLabel: 'Высокий',
      priorityClass: 'high',
    },
    {
      title: 'Вернуть пакет конференции',
      days: 15,
      comments: 34,
      priorityLabel: 'Низкий',
      priorityClass: 'low',
    },
  ];

  const completed = [
    {
      title: 'Подобрать детскую активность',
      days: 3,
      comments: 12,
      priorityLabel: 'Низкий',
      priorityClass: 'low',
    },
  ];

  const attachments = [
    { name: 'Медицинское_предписание.docx', time: '12:32, 22 августа' },
    { name: 'Запись_к_врачу.pdf', time: '14:35, 24 августа' },
  ];

  const comments = [
    {
      author: 'Иван Смирнов',
      date: '17 февраля 2024',
      message: 'Мне нужен полный план питания.',
    },
    { author: 'Иван Смирнов', date: 'Только что', message: 'Есть ли обновление по задаче?' },
  ];
</script>

<section class="page events">
  <header class="page-head">
    <div>
      <p class="eyebrow">Планировщик</p>
      <h1>Мои события</h1>
      <p class="sub">Контролируйте встречи, комментарии и вложения на единой доске планирования.</p>
    </div>
  </header>

  <div class="events-grid">
    <article class="card board">
      <div class="filters">
        <button type="button" class="active">Все</button>
        <button type="button">Удаленно</button>
        <button type="button">Очно</button>
      </div>

      <section class="lane">
        <h3>К выполнению <span>{todo.length}</span></h3>
        {#each todo as item}
          <div class="task-card">
            <div class="task-row">
              <strong>{item.title}</strong>
              <span class="priority {item.priorityClass}">{item.priorityLabel} приоритет</span>
            </div>
            <p>{item.days} дн. осталось | {item.comments} комментариев</p>
          </div>
        {/each}
      </section>

      <section class="lane">
        <h3>В процессе <span>{inProgress.length}</span></h3>
        {#each inProgress as item}
          <div class="task-card">
            <div class="task-row">
              <strong>{item.title}</strong>
              <span class="priority {item.priorityClass}">{item.priorityLabel} приоритет</span>
            </div>
            <p>{item.days} дн. осталось | {item.comments} комментариев</p>
          </div>
        {/each}
      </section>

      <section class="lane">
        <h3>Завершено <span>{completed.length}</span></h3>
        {#each completed as item}
          <div class="task-card">
            <div class="task-row">
              <strong>{item.title}</strong>
              <span class="priority {item.priorityClass}">{item.priorityLabel} приоритет</span>
            </div>
            <p>{item.days} дн. осталось | {item.comments} комментариев</p>
          </div>
        {/each}
      </section>
    </article>

    <aside class="card details">
      <p class="eyebrow">Прием</p>
      <h2>Запланируйте мне прием у эндокринолога</h2>
      <div class="chips">
        <span>Высокий приоритет</span>
        <span>10-14 июля</span>
      </div>

      <div class="focus-time">
        <p>Время, затраченное на задачу</p>
        <strong>12:45:00</strong>
      </div>

      <section class="copy">
        <h3>Описание</h3>
        <p>
          Специализация включает диагностику и лечение заболеваний эндокринной системы, включая
          гормональный фон, обмен веществ и процессы роста.
        </p>
      </section>

      <section class="copy">
        <h3>Вложения</h3>
        <ul>
          {#each attachments as file}
            <li>
              <div>
                <p>{file.name}</p>
                <small>{file.time}</small>
              </div>
              <div class="file-actions">
                <button type="button">Открыть</button>
                <button type="button">Скачать</button>
              </div>
            </li>
          {/each}
        </ul>
      </section>

      <section class="copy">
        <h3>Комментарии</h3>
        <ul class="comments">
          {#each comments as comment}
            <li>
              <div class="avatar">{comment.author[0]}</div>
              <div>
                <p class="meta">{comment.author} | {comment.date}</p>
                <p>{comment.message}</p>
              </div>
            </li>
          {/each}
        </ul>
      </section>
    </aside>
  </div>
</section>

<style>
  .events-grid {
    display: grid;
    gap: 0.8rem;
    grid-template-columns: 1.35fr 1fr;
  }

  .board {
    padding: 1rem;
  }

  .filters {
    display: inline-flex;
    gap: 0.35rem;
    padding: 0.3rem;
    border-radius: 999px;
    background: #f3f5f4;
    border: 1px solid #e4ece7;
  }

  .filters button {
    border: none;
    border-radius: 999px;
    padding: 0.45rem 0.8rem;
    background: transparent;
    color: var(--text-dim);
    font-weight: 700;
    font-size: 0.76rem;
    cursor: pointer;
  }

  .filters button.active {
    background: #fff;
    color: var(--text-main);
    box-shadow: 0 2px 8px rgba(18, 33, 27, 0.08);
  }

  .lane {
    margin-top: 1rem;
    display: grid;
    gap: 0.6rem;
  }

  .lane h3 {
    font-size: 0.8rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--text-dim);
    display: inline-flex;
    gap: 0.3rem;
    align-items: center;
  }

  .lane h3 span {
    display: inline-grid;
    place-items: center;
    width: 1.3rem;
    height: 1.3rem;
    border-radius: 999px;
    background: #f1f4f2;
    color: #4f665b;
    font-size: 0.7rem;
    font-weight: 700;
  }

  .task-card {
    border: 1px solid #e3ebe6;
    border-radius: 14px;
    padding: 0.8rem;
    background: linear-gradient(180deg, #ffffff 0%, #fbfcfb 100%);
  }

  .task-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0.55rem;
  }

  .task-row strong {
    font-size: 0.95rem;
    font-family: 'Sora', sans-serif;
  }

  .task-card p {
    margin-top: 0.3rem;
    color: var(--text-dim);
    font-size: 0.8rem;
    font-weight: 600;
  }

  .priority {
    border-radius: 999px;
    padding: 0.24rem 0.5rem;
    font-size: 0.67rem;
    font-weight: 700;
    text-transform: lowercase;
  }

  .priority.high {
    color: #8b1d43;
    background: #f8d9e5;
  }

  .priority.medium {
    color: #584192;
    background: #e8ddff;
  }

  .priority.low {
    color: #275733;
    background: #d7f0d6;
  }

  .details {
    padding: 1rem;
    display: grid;
    gap: 1rem;
  }

  .details h2 {
    font-size: clamp(1.25rem, 2vw, 1.6rem);
    line-height: 1.2;
  }

  .chips {
    display: flex;
    gap: 0.45rem;
    flex-wrap: wrap;
  }

  .chips span {
    border-radius: 999px;
    padding: 0.32rem 0.65rem;
    font-size: 0.72rem;
    font-weight: 700;
    color: #40574c;
    background: #eef6f1;
    border: 1px solid #ddece4;
  }

  .focus-time {
    border-radius: 14px;
    border: 1px solid #e6d8f8;
    background: linear-gradient(120deg, #f6edf8 0%, #efe6f7 100%);
    padding: 0.7rem 0.8rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0.75rem;
  }

  .focus-time p {
    color: #644d76;
    font-size: 0.8rem;
    font-weight: 700;
  }

  .focus-time strong {
    font-family: 'Sora', sans-serif;
    font-size: 1.2rem;
  }

  .copy {
    display: grid;
    gap: 0.5rem;
  }

  .copy h3 {
    font-size: 0.92rem;
  }

  .copy p {
    color: var(--text-soft);
    line-height: 1.5;
  }

  .copy ul {
    margin: 0;
    padding: 0;
    list-style: none;
    display: grid;
    gap: 0.5rem;
  }

  .copy li {
    display: flex;
    justify-content: space-between;
    gap: 0.6rem;
    border: 1px solid #e4ebe6;
    border-radius: 12px;
    padding: 0.55rem 0.65rem;
    align-items: center;
  }

  .copy li p {
    font-weight: 700;
    font-size: 0.86rem;
  }

  .copy li small {
    color: var(--text-dim);
    font-weight: 600;
    font-size: 0.75rem;
  }

  .file-actions {
    display: flex;
    gap: 0.38rem;
  }

  .file-actions button {
    border: 1px solid #dce8e1;
    background: #f7faf8;
    color: var(--text-soft);
    border-radius: 999px;
    padding: 0.3rem 0.6rem;
    font-size: 0.72rem;
    font-weight: 700;
    cursor: pointer;
  }

  .comments li {
    border: none;
    padding: 0;
    align-items: flex-start;
  }

  .avatar {
    width: 1.8rem;
    height: 1.8rem;
    border-radius: 999px;
    display: grid;
    place-items: center;
    font-weight: 700;
    background: linear-gradient(150deg, #ffd5be 0%, #ffbc9e 100%);
    color: #6d2d0f;
    flex-shrink: 0;
  }

  .meta {
    font-size: 0.76rem;
    color: var(--text-dim);
    margin-bottom: 0.15rem;
    font-weight: 700;
  }

  @media (max-width: 1080px) {
    .events-grid {
      grid-template-columns: 1fr;
    }
  }
</style>
