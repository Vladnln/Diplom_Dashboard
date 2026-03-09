<script>
  const quickFolders = [
    { name: 'Учебные материалы', size: '2.3 ГБ', items: '23 файла' },
    { name: 'Исходники', size: '1.2 МБ', items: '1 файл' },
    { name: 'Активы', size: '241 МБ', items: '8 файлов' },
    { name: 'Презентация кафедры', size: '12.3 МБ', items: 'pptx' },
  ];

  const files = [
    { name: 'Документы', sharing: 'Публичный', size: '4.5 МБ', modified: '10 апр 2022' },
    { name: 'Шрифты', sharing: 'Публичный', size: '2.5 МБ', modified: '2 апр 2022' },
    { name: 'Исходники', sharing: 'Команда +4', size: '1.2 МБ', modified: 'Вчера' },
    { name: 'Примеры', sharing: 'Публичный', size: '12.2 МБ', modified: 'Вчера' },
    { name: 'Readme.md', sharing: 'Публичный', size: '2 КБ', modified: '12 окт 2021' },
    { name: 'index.html', sharing: 'Публичный', size: '14 КБ', modified: '12 окт 2021' },
  ];

  const activity = [
    'Вы выдали доступ на редактирование Альберту',
    'Вы выдали доступ на редактирование Ивану',
    'Вы добавили тег "Работа"',
    'Вы изменили уровень доступа Эрика',
  ];
</script>

<section class="page files">
  <header class="page-head">
    <div>
      <p class="eyebrow">Облачное хранилище</p>
      <h1>Файловый центр</h1>
      <p class="sub">Организуйте файлы кафедры, смотрите активность и управляйте тегами.</p>
    </div>
  </header>

  <div class="files-grid">
    <div class="main-column">
      <article class="card quick-access">
        <div class="title-row">
          <h3>Быстрый доступ</h3>
        </div>
        <div class="quick-grid">
          {#each quickFolders as folder}
            <div class="folder">
              <div class="folder-icon"></div>
              <p>{folder.name}</p>
              <small>{folder.size} | {folder.items}</small>
            </div>
          {/each}
        </div>
      </article>

      <article class="card file-table">
        <div class="title-row">
          <h3>Главная / Концепт шрифта </h3>
          <button type="button">+ Добавить</button>
        </div>

        <div class="table-wrap">
          <table>
            <thead>
              <tr>
                <th>Имя</th>
                <th>Доступ</th>
                <th>Размер</th>
                <th>Изменен</th>
              </tr>
            </thead>
            <tbody>
              {#each files as row}
                <tr class:highlighted={row.name === 'Исходники'}>
                  <td>{row.name}</td>
                  <td>{row.sharing}</td>
                  <td>{row.size}</td>
                  <td>{row.modified}</td>
                </tr>
              {/each}
            </tbody>
          </table>
        </div>
      </article>
    </div>

    <aside class="card side-panel">
      <h3>Исходники</h3>
      <p class="meta">1.2 МБ | Вчера | 1 файл</p>

      <div class="tags">
        <span>Работа</span>
        <span>Исходник</span>
        <span>Шрифт</span>
      </div>

      <div class="share">
        <p>Совместный доступ</p>
        <div class="avatars">
          <span>АН</span>
          <span>ДН</span>
          <span>ИО</span>
          <span>+1</span>
        </div>
      </div>

      <section class="activity">
        <h4>Активность</h4>
        <ul>
          {#each activity as item}
            <li>{item}</li>
          {/each}
        </ul>
      </section>
    </aside>
  </div>
</section>

<style>
  .files-grid {
    display: grid;
    gap: 0.8rem;
    grid-template-columns: 1.4fr 0.68fr;
  }

  .main-column {
    display: grid;
    gap: 0.8rem;
  }

  .quick-access,
  .file-table,
  .side-panel {
    padding: 1rem;
  }

  .title-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0.6rem;
  }

  .quick-grid {
    margin-top: 0.9rem;
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    gap: 0.6rem;
  }

  .folder {
    border: 1px solid #e3ebe6;
    border-radius: 13px;
    padding: 0.75rem;
    background: linear-gradient(180deg, #ffffff 0%, #fbfdfb 100%);
  }

  .folder-icon {
    width: 1.6rem;
    height: 1.15rem;
    border-radius: 0.3rem;
    background: linear-gradient(145deg, #2963ff 0%, #3d7bff 100%);
    position: relative;
  }

  .folder-icon::before {
    content: '';
    position: absolute;
    width: 0.72rem;
    height: 0.22rem;
    top: -0.15rem;
    left: 0.15rem;
    border-radius: 0.2rem 0.2rem 0 0;
    background: #4f83ff;
  }

  .folder p {
    margin-top: 0.6rem;
    font-weight: 700;
    font-size: 0.9rem;
  }

  .folder small {
    color: var(--text-dim);
    font-weight: 600;
    font-size: 0.75rem;
  }

  .file-table button {
    border: none;
    border-radius: 10px;
    background: linear-gradient(150deg, #2d63ff 0%, #355cf0 100%);
    color: #fff;
    font-weight: 700;
    padding: 0.45rem 0.8rem;
    cursor: pointer;
  }

  .table-wrap {
    margin-top: 0.85rem;
    overflow-x: auto;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    min-width: 560px;
  }

  th,
  td {
    text-align: left;
    padding: 0.65rem 0.55rem;
    border-bottom: 1px solid #e7ede9;
    font-size: 0.84rem;
  }

  th {
    color: var(--text-dim);
    font-size: 0.74rem;
    text-transform: uppercase;
    letter-spacing: 0.07em;
  }

  td {
    color: var(--text-soft);
    font-weight: 600;
  }

  tr.highlighted {
    background: #ebf3ff;
  }

  .side-panel {
    display: grid;
    align-content: start;
    gap: 1rem;
  }

  .meta {
    color: var(--text-dim);
    font-size: 0.8rem;
    font-weight: 600;
  }

  .tags,
  .avatars {
    display: flex;
    gap: 0.4rem;
    flex-wrap: wrap;
  }

  .tags span {
    border: 1px solid #d8e4ff;
    background: #edf3ff;
    color: #2c56aa;
    border-radius: 8px;
    padding: 0.24rem 0.45rem;
    font-weight: 700;
    font-size: 0.7rem;
  }

  .share p {
    margin-bottom: 0.5rem;
    color: var(--text-dim);
    font-weight: 700;
    font-size: 0.8rem;
  }

  .avatars span {
    width: 1.9rem;
    height: 1.9rem;
    border-radius: 999px;
    display: grid;
    place-items: center;
    background: #edf2ef;
    color: #496259;
    font-size: 0.68rem;
    font-weight: 700;
    font-family: 'Sora', sans-serif;
  }

  .activity h4 {
    font-size: 0.9rem;
    margin-bottom: 0.55rem;
  }

  .activity ul {
    margin: 0;
    padding: 0;
    list-style: none;
    display: grid;
    gap: 0.6rem;
  }

  .activity li {
    position: relative;
    padding-left: 0.9rem;
    color: var(--text-soft);
    font-size: 0.82rem;
    line-height: 1.35;
  }

  .activity li::before {
    content: '';
    position: absolute;
    left: 0;
    top: 0.45rem;
    width: 0.38rem;
    height: 0.38rem;
    border-radius: 999px;
    background: linear-gradient(150deg, #3f7cff 0%, #274ed1 100%);
  }

  @media (max-width: 1240px) {
    .quick-grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }
  }

  @media (max-width: 1080px) {
    .files-grid {
      grid-template-columns: 1fr;
    }
  }

  @media (max-width: 640px) {
    .quick-grid {
      grid-template-columns: 1fr;
    }
  }
</style>
