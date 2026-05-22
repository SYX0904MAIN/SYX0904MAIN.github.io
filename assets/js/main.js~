document.addEventListener('DOMContentLoaded', () => {

  // ---------- 左侧侧边栏 TOC ----------
  const sidebar = document.getElementById('sidebar-toc');
  const toggleBtn = document.getElementById('sidebar-toggle-btn');
  const overlay = document.getElementById('sidebar-overlay');
  const postContent = document.getElementById('post-content');

  // 生成文章内 TOC
  if (postContent && sidebar) {
    const headings = postContent.querySelectorAll('h2, h3');
    const tocList = document.getElementById('toc-list');
    headings.forEach((heading, index) => {
      // 确保每个标题有 id（kramdown 默认会生成，但手动保险）
      if (!heading.id) {
        heading.id = 'heading-' + index;
      }
      const li = document.createElement('li');
      const a = document.createElement('a');
      a.href = '#' + heading.id;
      a.textContent = heading.textContent;
      a.style.paddingLeft = (heading.tagName === 'H3' ? '1.5rem' : '0.5rem');
      a.addEventListener('click', (e) => {
        // 点击后关闭侧边栏（移动端体验更好）
        closeSidebar();
      });
      li.appendChild(a);
      tocList.appendChild(li);
    });
  }

  // 打开侧边栏
  function openSidebar() {
    sidebar.classList.add('active');
    overlay.classList.add('active');
    document.body.classList.add('sidebar-active');
  }

  // 关闭侧边栏
  function closeSidebar() {
    sidebar.classList.remove('active');
    overlay.classList.remove('active');
    document.body.classList.remove('sidebar-active');
  }

  // 点击汉堡按钮切换
  toggleBtn.addEventListener('click', () => {
    sidebar.classList.contains('active') ? closeSidebar() : openSidebar();
  });

  // 点击遮罩关闭
  overlay.addEventListener('click', closeSidebar);

  // 按 Esc 关闭侧边栏
  document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape' && sidebar.classList.contains('active')) {
      closeSidebar();
    }
  });


  // ---------- 全局文章目录（Ctrl+I） ----------
  const globalOverlay = document.getElementById('global-toc-overlay');
  const closeGlobalBtn = document.getElementById('close-global-toc');

  function openGlobalToc() {
    globalOverlay.classList.add('active');
  }

  function closeGlobalToc() {
    globalOverlay.classList.remove('active');
  }

  // Ctrl+I 切换
  document.addEventListener('keydown', (e) => {
    if (e.ctrlKey && e.key === 'i') {
      e.preventDefault();
      globalOverlay.classList.contains('active') ? closeGlobalToc() : openGlobalToc();
    }
  });

  // 点击关闭按钮
  if (closeGlobalBtn) {
    closeGlobalBtn.addEventListener('click', closeGlobalToc);
  }

  // 点击全局目录中的链接后自动关闭
  globalOverlay.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => {
      closeGlobalToc();
    });
  });

  // 按 Esc 关闭全局目录
  document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape' && globalOverlay.classList.contains('active')) {
      closeGlobalToc();
    }
  });

});