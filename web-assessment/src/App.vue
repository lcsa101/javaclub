<template>
  <div class="app">
    <!-- 顶部滚动进度条 -->
    <div class="scroll-progress" :style="{ width: scrollProgress + '%' }"></div>

    <!-- 鼠标跟随光斑 -->
    <div class="cursor-light" ref="cursorLight"></div>

    <!-- 背景层 -->
    <div class="bg-layer">
      <div class="bg-grid"></div>
      <div class="blob blob-1"></div>
      <div class="blob blob-2"></div>
      <div class="blob blob-3"></div>
      <div class="bg-noise"></div>
    </div>

    <!-- 页头 -->
    <header class="site-header">
      <div class="container nav-container">
        <a class="logo" href="#top" @click.prevent="scrollTo('top')">
          <span class="logo-mark">
            <span class="logo-ring"></span>
            <span class="logo-core"></span>
          </span>
          <span class="logo-text">林子杰</span>
          <span class="logo-sub">/ 主页</span>
        </a>

        <nav class="nav-links">
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="'#' + item.id"
            :class="{ active: activeSection === item.id }"
            @click.prevent="scrollTo(item.id)"
          >
            {{ item.name }}
          </a>
        </nav>

        <div class="nav-actions">
          <button class="theme-btn" type="button" @click="toggleTheme" aria-label="切换主题">
            <svg v-if="isDark" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="4" />
              <path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M4.93 19.07l1.41-1.41M17.66 6.34l1.41-1.41" />
            </svg>
            <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
            </svg>
          </button>
        </div>
      </div>
    </header>

    <!-- Hero -->
    <section id="top" class="hero">
      <div class="container hero-grid">
        <div class="hero-left">
          <div class="hero-badge">
            <span class="badge-dot"></span>
            JAVA 俱乐部招新 · 个人主页
          </div>

          <h1 class="hero-title">
            <span class="title-line">你好，我是</span>
            <span class="title-name">
              林子杰
              <svg class="title-underline" viewBox="0 0 300 12" preserveAspectRatio="none">
                <path d="M2 8 Q 80 2, 150 6 T 298 4" stroke="url(#underline-grad)" stroke-width="3" fill="none" stroke-linecap="round" />
                <defs>
                  <linearGradient id="underline-grad" x1="0" y1="0" x2="1" y2="0">
                    <stop offset="0%" stop-color="#6366f1" />
                    <stop offset="50%" stop-color="#ec4899" />
                    <stop offset="100%" stop-color="#f59e0b" />
                  </linearGradient>
                </defs>
              </svg>
            </span>
          </h1>

          <p class="hero-sub">
            <span>{{ typedText }}</span>
            <span class="type-cursor" :class="{ blinking: typing }">|</span>
          </p>

          <p class="hero-desc">
            软件工程2504班学生，正在学习 Java 与 Web 前端，同时自学 CS106B。
            想在这里把兴趣变成能力，把想法变成看得见的东西。
          </p>

          <div class="hero-cta">
            <a href="#about" class="btn-primary" @click.prevent="scrollTo('about')">
              了解我
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M5 12h14M12 5l7 7-7 7" />
              </svg>
            </a>
            <a href="#future" class="btn-ghost" @click.prevent="scrollTo('future')">我的规划</a>
          </div>

          <div class="hero-stats">
            <div class="stat">
              <strong>2504</strong>
              <span>班级</span>
            </div>
            <div class="stat-divider"></div>
            <div class="stat">
              <strong>7+</strong>
              <span>在学技能</span>
            </div>
            <div class="stat-divider"></div>
            <div class="stat">
              <strong>3</strong>
              <span>发展方向</span>
            </div>
          </div>
        </div>

        <div class="hero-right">
          <div class="hero-visual-wrap">
            <div class="orbit orbit-1"><span class="orbit-dot dot-purple"></span></div>
            <div class="orbit orbit-2"><span class="orbit-dot dot-pink"></span></div>
            <div class="orbit orbit-3"><span class="orbit-dot dot-amber"></span></div>

            <div class="glass-card">
              <div class="gc-header">
                <div class="gc-label-title">学习状态</div>
                <div class="gc-status">
                  <span class="status-pulse"></span>
                  正在进行
                </div>
              </div>

              <!-- 进度环 -->
              <div class="progress-ring-wrap">
                <svg class="progress-ring" viewBox="0 0 120 120">
                  <defs>
                    <linearGradient id="ring-g" x1="0" y1="0" x2="1" y2="1">
                      <stop offset="0%" stop-color="#7c3aed" />
                      <stop offset="100%" stop-color="#ec4899" />
                    </linearGradient>
                  </defs>
                  <circle cx="60" cy="60" r="50" stroke="var(--divider)" stroke-width="8" fill="none" />
                  <circle
                    class="progress-circle"
                    cx="60" cy="60" r="50"
                    stroke="url(#ring-g)"
                    stroke-width="8"
                    fill="none"
                    stroke-linecap="round"
                    :stroke-dasharray="314"
                    :stroke-dashoffset="314 - 314 * 0.48"
                    transform="rotate(-90 60 60)"
                  />
                </svg>
                <div class="progress-text">
                  <strong>48%</strong>
                  <span>本学期进度</span>
                </div>
              </div>

              <!-- 状态清单 -->
              <div class="gc-list">
                <div class="gc-row">
                  <div class="gc-row-dot dot-1"></div>
                  <div>
                    <span class="gc-row-label">现在在学</span>
                    <strong>Java · Web · CS106B</strong>
                  </div>
                </div>
                <div class="gc-row">
                  <div class="gc-row-dot dot-2"></div>
                  <div>
                    <span class="gc-row-label">下一步</span>
                    <strong>完成第一个完整小项目</strong>
                  </div>
                </div>
                <div class="gc-row">
                  <div class="gc-row-dot dot-3"></div>
                  <div>
                    <span class="gc-row-label">QQ</span>
                    <strong>731583180</strong>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="scroll-hint">
        <span>向下滚动</span>
        <div class="scroll-line"></div>
      </div>
    </section>

    <!-- 01 关于我 -->
    <section id="about" class="section">
      <div class="container">
        <div class="section-head reveal">
          <div class="section-num">01</div>
          <div>
            <h2 class="section-title">关于我</h2>
            <p class="section-sub">学习背景、兴趣爱好、个人特点，快速了解我</p>
          </div>
        </div>

        <div class="about-grid">
          <div class="about-intro reveal">
            <p class="about-lead">
              我是 <em>林子杰</em>，软件工程2504班学生。
              在按计划学习专业课的同时自学 CS106B，希望打好编程基础。
            </p>
            <p class="about-text">
              性格上偏计划型，习惯把大目标拆成一个个小任务。
              遇到问题会先查文档，再请教同学，最后整理成笔记。
              业余喜欢打乒乓球，运动让我保持专注和节奏感。
              接下来希望能把兴趣变成能力，一步步做出自己的作品。
            </p>
          </div>

          <div class="about-cards reveal" style="--delay: 0.15s">
            <div class="mini-card">
              <div class="mini-icon icon-pingpong">
                <svg viewBox="0 0 40 40" fill="none">
                  <circle cx="18" cy="16" r="11" fill="currentColor" opacity="0.9" />
                  <circle cx="18" cy="16" r="7" fill="#fff" opacity="0.55" />
                  <rect x="15.5" y="26" width="5" height="11" rx="2.5" fill="currentColor" />
                </svg>
              </div>
              <div>
                <h4>兴趣爱好</h4>
                <p>打乒乓球</p>
              </div>
            </div>

            <div class="mini-card">
              <div class="mini-icon icon-plan">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <rect x="3" y="4" width="18" height="18" rx="2" />
                  <path d="M16 2v4M8 2v4M3 10h18" />
                  <path d="M8 14h.01M12 14h.01M16 14h.01" />
                </svg>
              </div>
              <div>
                <h4>个人特点</h4>
                <p>计划型 · 执行力强</p>
              </div>
            </div>

            <div class="mini-card">
              <div class="mini-icon icon-book">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20" />
                  <path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z" />
                </svg>
              </div>
              <div>
                <h4>目前在做</h4>
                <p>自学 CS106B</p>
              </div>
            </div>
          </div>
        </div>

        <div class="skills-wrap reveal" style="--delay: 0.2s">
          <div class="skills-head">
            <h4>技能基础</h4>
            <span>不断更新中</span>
          </div>
          <div class="skill-tags">
            <span class="s-tag t-purple">HTML</span>
            <span class="s-tag t-purple">CSS</span>
            <span class="s-tag t-purple">JavaScript</span>
            <span class="s-tag t-pink">C 语言</span>
            <span class="s-tag t-pink">C++ 基础</span>
            <span class="s-tag t-amber">Java 基础</span>
            <span class="s-tag t-amber">CS106B</span>
          </div>
        </div>
      </div>
    </section>

    <!-- 02 未来规划 -->
    <section id="future" class="section">
      <div class="container">
        <div class="section-head reveal">
          <div class="section-num">02</div>
          <div>
            <h2 class="section-title">未来规划</h2>
            <p class="section-sub">点击下方标签切换不同发展方向</p>
          </div>
        </div>

        <div class="tab-bar reveal">
          <button
            v-for="tab in futureTabs"
            :key="tab.id"
            class="tab-btn"
            :class="{ active: activeTab === tab.id }"
            type="button"
            @click="activeTab = tab.id"
          >
            <span class="tab-dot" :class="'tab-dot-' + tab.color"></span>
            {{ tab.name }}
          </button>
          <div class="tab-indicator" :style="tabIndicatorStyle"></div>
        </div>

        <transition name="tab-fade" mode="out-in">
          <div class="tab-panel" :key="activeTab">
            <div class="tp-left">
              <div class="tp-icon" :class="'tp-icon-' + currentTab.color">
                <svg v-if="currentTab.icon === 'book'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20" />
                  <path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z" />
                </svg>
                <svg v-else-if="currentTab.icon === 'rocket'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M4.5 16.5c-1.5 1.26-2 5-2 5s3.74-.5 5-2c.71-.84.7-2.13-.09-2.91a2.18 2.18 0 0 0-2.91-.09z" />
                  <path d="M12 15l-3-3a22 22 0 0 1 2-3.95A12.88 12.88 0 0 1 22 2c0 2.72-.78 7.5-6 11a22.35 22.35 0 0 1-4 2z" />
                  <path d="M9 12H4s.55-3.03 2-4c1.62-1.08 5 0 5 0" />
                  <path d="M12 15v5s3.03-.55 4-2c1.08-1.62 0-5 0-5" />
                </svg>
                <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
                  <circle cx="12" cy="8" r="6" />
                  <path d="M15.477 12.89 17 22l-5-3-5 3 1.523-9.11" />
                </svg>
              </div>
              <h3>{{ currentTab.title }}</h3>
              <p class="tp-reason">{{ currentTab.reason }}</p>
            </div>

            <div class="tp-right">
              <div class="tp-goals-title">阶段目标</div>
              <ul class="tp-goals">
                <li v-for="(goal, i) in currentTab.goals" :key="i">
                  <span class="goal-num">{{ String(i + 1).padStart(2, '0') }}</span>
                  {{ goal }}
                </li>
              </ul>
            </div>
          </div>
        </transition>

        <div class="timeline-title reveal">
          <h3>时间轴</h3>
        </div>

        <div class="timeline">
          <div class="tl-item reveal">
            <div class="tl-marker">
              <span class="tl-dot dot-purple"></span>
              <span class="tl-line"></span>
            </div>
            <div class="tl-card">
              <div class="tl-top">
                <span class="tl-phase">大二下</span>
                <span class="tl-tag">基础</span>
              </div>
              <h4>打牢 Java 与 Web 基础</h4>
              <p>掌握 Java 基础语法、集合与 IO，能独立完成一个课程小项目；Web 前端能使用 Vue3 完成中小型页面。</p>
            </div>
          </div>

          <div class="tl-item reveal" style="--delay: 0.05s">
            <div class="tl-marker">
              <span class="tl-dot dot-pink"></span>
              <span class="tl-line"></span>
            </div>
            <div class="tl-card">
              <div class="tl-top">
                <span class="tl-phase">大三上</span>
                <span class="tl-tag">项目</span>
              </div>
              <h4>项目实践与方向确认</h4>
              <p>完成一个后端 + 前端的小项目；参加校内或俱乐部内部的小型竞赛积累经验，同时确定考研目标或就业方向。</p>
            </div>
          </div>

          <div class="tl-item reveal" style="--delay: 0.1s">
            <div class="tl-marker">
              <span class="tl-dot dot-amber"></span>
              <span class="tl-line"></span>
            </div>
            <div class="tl-card">
              <div class="tl-top">
                <span class="tl-phase">大三下</span>
                <span class="tl-tag">冲刺</span>
              </div>
              <h4>复习与实习并行</h4>
              <p>考研方向开始数学、英语和专业课复习；就业方向投递暑期实习，同步准备简历与项目文档。</p>
            </div>
          </div>

          <div class="tl-item reveal" style="--delay: 0.15s">
            <div class="tl-marker">
              <span class="tl-dot dot-purple"></span>
            </div>
            <div class="tl-card">
              <div class="tl-top">
                <span class="tl-phase">大四</span>
                <span class="tl-tag">收尾</span>
              </div>
              <h4>冲刺与收尾</h4>
              <p>考研冲刺或秋招投递，同时整理作品集、项目文档和竞赛经历，为毕业做最后准备。</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 03 加入俱乐部 -->
    <section id="club" class="section">
      <div class="container">
        <div class="section-head reveal">
          <div class="section-num">03</div>
          <div>
            <h2 class="section-title">加入俱乐部想学什么</h2>
            <p class="section-sub">点击卡片标题，展开或收起具体学习目标</p>
          </div>
        </div>

        <div class="club-grid">
          <article
            v-for="(item, i) in clubItems"
            :key="item.key"
            class="club-card reveal"
            :class="{ open: openClub[item.key] }"
            :style="{ '--delay': i * 0.08 + 's' }"
          >
            <div class="cc-glow" :class="'glow-' + item.color"></div>

            <button class="cc-header" type="button" @click="toggleClub(item.key)">
              <div class="cc-top">
                <span class="cc-num">{{ String(i + 1).padStart(2, '0') }}</span>
                <div class="cc-icon" :class="'cc-icon-' + item.color">
                  <svg v-if="item.icon === 'db'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round">
                    <ellipse cx="12" cy="5" rx="9" ry="3" />
                    <path d="M3 5v14c0 1.66 4.03 3 9 3s9-1.34 9-3V5" />
                    <path d="M3 12c0 1.66 4.03 3 9 3s9-1.34 9-3" />
                  </svg>
                  <svg v-else-if="item.icon === 'web'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round">
                    <rect x="2" y="3" width="20" height="14" rx="2" />
                    <line x1="8" y1="21" x2="16" y2="21" />
                    <line x1="12" y1="17" x2="12" y2="21" />
                  </svg>
                  <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2" />
                    <circle cx="9" cy="7" r="4" />
                    <path d="M23 21v-2a4 4 0 0 0-3-3.87" />
                    <path d="M16 3.13a4 4 0 0 1 0 7.75" />
                  </svg>
                </div>
              </div>
              <h3>{{ item.title }}</h3>
              <p class="cc-brief">{{ item.brief }}</p>
              <span class="cc-toggle-icon">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <polyline points="6 9 12 15 18 9" />
                </svg>
              </span>
            </button>

            <transition name="fold">
              <div v-show="openClub[item.key]" class="cc-body">
                <ul class="cc-list">
                  <li v-for="(goal, j) in item.goals" :key="j">{{ goal }}</li>
                </ul>
              </div>
            </transition>
          </article>
        </div>
      </div>
    </section>

    <!-- 04 竞赛目标 -->
    <section id="contest" class="section">
      <div class="container">
        <div class="contest-banner reveal">
          <div class="cb-bg"></div>
          <div class="cb-left">
            <div class="section-num section-num-inline">04</div>
            <h2 class="cb-title">竞赛目标</h2>
            <p class="cb-desc">
              在打好基础之后，参加一些编程或项目类比赛来提升自己。
              通过比赛检验学习成果、发现短板，在团队协作中积累项目经验，
              让简历和作品集更有说服力。
            </p>
            <div class="cb-points">
              <div class="cb-point"><span class="bp-dot"></span>参加校内程序设计或算法比赛</div>
              <div class="cb-point"><span class="bp-dot"></span>参与俱乐部内部小型项目或竞赛</div>
              <div class="cb-point"><span class="bp-dot"></span>每次比赛后复盘并整理成笔记</div>
            </div>
          </div>
          <div class="cb-right">
            <svg viewBox="0 0 200 200" class="trophy-svg">
              <defs>
                <linearGradient id="tr-g" x1="0" y1="0" x2="1" y2="1">
                  <stop offset="0%" stop-color="#fbbf24" />
                  <stop offset="100%" stop-color="#f59e0b" />
                </linearGradient>
                <linearGradient id="tr-g2" x1="0" y1="0" x2="1" y2="1">
                  <stop offset="0%" stop-color="#fde68a" />
                  <stop offset="100%" stop-color="#fbbf24" />
                </linearGradient>
              </defs>
              <circle cx="100" cy="100" r="90" fill="url(#tr-g)" opacity="0.08" />
              <circle cx="100" cy="100" r="70" fill="url(#tr-g)" opacity="0.06" />
              <path d="M60 40h80v30a40 40 0 0 1-80 0V40z" fill="url(#tr-g)" />
              <path d="M60 48H38v10a24 24 0 0 0 24 24" stroke="url(#tr-g2)" stroke-width="5" fill="none" stroke-linecap="round" />
              <path d="M140 48h22v10a24 24 0 0 1-24 24" stroke="url(#tr-g2)" stroke-width="5" fill="none" stroke-linecap="round" />
              <rect x="92" y="108" width="16" height="28" fill="url(#tr-g)" />
              <rect x="78" y="136" width="44" height="10" rx="3" fill="url(#tr-g)" />
              <rect x="66" y="146" width="68" height="16" rx="4" fill="url(#tr-g)" />
              <circle cx="100" cy="60" r="6" fill="#fff" opacity="0.9" />
            </svg>
          </div>
        </div>
      </div>
    </section>

    <!-- 页尾 -->
    <footer class="site-footer">
      <div class="container footer-inner">
        <div class="footer-left">
          <div class="footer-logo">林子杰</div>
          <p>© 2026 · JAVA 俱乐部招新考核作品</p>
        </div>
        <div class="footer-right">
          <span>QQ</span>
          <strong>731583180</strong>
        </div>
      </div>
    </footer>

    <!-- 回到顶部 -->
    <button class="back-top" :class="{ show: showBackTop }" type="button" @click="backTop" aria-label="回到顶部">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M12 19V5M5 12l7-7 7 7" />
      </svg>
    </button>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

/* ---------- 状态 ---------- */
const isDark = ref(false)
const showBackTop = ref(false)
const activeSection = ref('top')
const scrollProgress = ref(0)
const cursorLight = ref(null)

/* 打字机 */
const typedText = ref('')
const typing = ref(true)
const fullText = '把想法，变成看得见的东西。'

/* Tab */
const activeTab = ref('kaoyan')
const futureTabs = [
  {
    id: 'kaoyan',
    name: '考研深造',
    color: 'purple',
    icon: 'book',
    title: '考研深造',
    reason: '我对后端开发和系统设计感兴趣，希望通过读研补足计算机基础，未来进入更看重工程能力的岗位。',
    goals: [
      '大二结束前，Java 与 Web 基础达到能独立做小项目的水平。',
      '大三上学期确定目标院校与专业方向。',
      '大三下至大四上完成数学、英语、专业课的一轮复习。'
    ]
  },
  {
    id: 'job',
    name: '就业实践',
    color: 'pink',
    icon: 'rocket',
    title: '就业实践',
    reason: '如果考研风险较大，我希望凭借项目经历和实习经历进入 Java 后端或 Web 开发岗位。',
    goals: [
      '完成一个后端 + 前端的小项目，形成作品集。',
      '大三暑假争取一段开发相关实习。',
      '整理简历、项目文档与常见面试题。'
    ]
  },
  {
    id: 'contest',
    name: '以赛促学',
    color: 'amber',
    icon: 'trophy',
    title: '以赛促学',
    reason: '比赛能给我明确的目标和反馈，把零散的知识串成完整的项目能力，也是检验学习成果的好方式。',
    goals: [
      '至少参加一次校内程序设计或算法比赛。',
      '参与俱乐部内部的项目或小型竞赛。',
      '每次比赛后复盘，整理成笔记。'
    ]
  }
]

const currentTab = computed(() =>
  futureTabs.find(t => t.id === activeTab.value) || futureTabs[0]
)

const tabIndicatorStyle = computed(() => {
  const idx = futureTabs.findIndex(t => t.id === activeTab.value)
  const w = 100 / futureTabs.length
  return {
    width: `calc(${w}% - 0.27rem)`,
    transform: `translateX(calc(${idx * 100}% + ${idx * 0.54}rem))`
  }
})

/* 俱乐部折叠 */
const openClub = ref({
  java: true,
  web: false,
  contest: false
})

const clubItems = [
  {
    key: 'java',
    color: 'purple',
    icon: 'db',
    title: 'Java 与后端开发',
    brief: '掌握 Java 集合、IO、多线程基础，学习后端开发流程。',
    goals: [
      '能读懂并写基础的后端代码',
      '独立完成一个小型接口项目',
      '理解数据库的基本操作与设计'
    ]
  },
  {
    key: 'web',
    color: 'pink',
    icon: 'web',
    title: 'Web 前端与工程化',
    brief: '使用 Vue3 完成中小型页面，理解组件化与状态管理。',
    goals: [
      '独立完成一个 Vue3 页面',
      '会用 Git 协作与部署项目',
      '理解前后端分离的基本流程'
    ]
  },
  {
    key: 'contest',
    color: 'amber',
    icon: 'team',
    title: '项目协作与竞赛',
    brief: '参与俱乐部内部项目或比赛，学习需求拆解与文档。',
    goals: [
      '至少参与 1 次团队项目',
      '学会写需求文档与接口文档',
      '和队友一起完成一次比赛'
    ]
  }
]

function toggleClub(key) {
  openClub.value[key] = !openClub.value[key]
}

/* 导航 */
const navItems = [
  { id: 'about', name: '关于我' },
  { id: 'future', name: '未来规划' },
  { id: 'club', name: '加入俱乐部' },
  { id: 'contest', name: '竞赛目标' }
]

/* ---------- 主题 ---------- */
function applyTheme(dark) {
  isDark.value = dark
  if (dark) {
    document.documentElement.setAttribute('data-theme', 'dark')
  } else {
    document.documentElement.removeAttribute('data-theme')
  }
}

function toggleTheme() {
  const next = !isDark.value
  applyTheme(next)
  localStorage.setItem('theme', next ? 'dark' : 'light')
}

/* ---------- 滚动 ---------- */
function scrollTo(id) {
  const el = document.getElementById(id)
  if (!el) return
  const y = el.getBoundingClientRect().top + window.scrollY - 70
  window.scrollTo({ top: y, behavior: 'smooth' })
}

function backTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function handleScroll() {
  const total = document.documentElement.scrollHeight - window.innerHeight
  scrollProgress.value = total > 0 ? (window.scrollY / total) * 100 : 0

  showBackTop.value = window.scrollY > 400

  const ids = ['top', ...navItems.map(i => i.id)]
  let current = 'top'
  ids.forEach(id => {
    const el = document.getElementById(id)
    if (el && window.scrollY >= el.offsetTop - 120) {
      current = id
    }
  })
  activeSection.value = current
}

function handleMouseMove(e) {
  if (!cursorLight.value) return
  cursorLight.value.style.transform =
    `translate(${e.clientX - 300}px, ${e.clientY - 300}px)`
}

/* ---------- 打字机 ---------- */
function startTyping() {
  let i = 0
  const timer = setInterval(() => {
    if (i < fullText.length) {
      typedText.value += fullText.charAt(i)
      i++
    } else {
      typing.value = false
      clearInterval(timer)
    }
  }, 80)
}

/* ---------- 生命周期 ---------- */
onMounted(() => {
  const saved = localStorage.getItem('theme')
  applyTheme(saved === 'dark')

  window.addEventListener('scroll', handleScroll)
  window.addEventListener('mousemove', handleMouseMove)
  handleScroll()

  startTyping()

  const items = document.querySelectorAll('.reveal')
  const observer = new IntersectionObserver(
    entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible')
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.12, rootMargin: '0px 0px -60px 0px' }
  )
  items.forEach(el => observer.observe(el))
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  window.removeEventListener('mousemove', handleMouseMove)
})
</script>