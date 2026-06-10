<template>
  <div class="app-wrapper">
    <!-- ═══════════════════════════ MOBILE OVERLAY ═══════════════════════════ -->
    <div v-if="isMobile" class="mobile-overlay">
      <div class="mobile-overlay-card">
        <div class="mobile-overlay-icon">
          <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <rect x="2" y="3" width="20" height="13" rx="2" ry="2"/>
            <polyline points="8 21 12 17 16 21"/>
            <line x1="12" y1="17" x2="12" y2="13"/>
          </svg>
        </div>
        <h1 class="mobile-overlay-title">Built for Desktop</h1>
        <p class="mobile-overlay-desc">
          <strong>NexBill POS</strong> is a Windows desktop application.
          This download page is best viewed on a <strong>laptop or desktop computer</strong> for the full experience.
        </p>
        <div class="mobile-overlay-tips">
          <div class="mobile-tip">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 9H4a2 2 0 0 0-2 2v.5A2.5 2.5 0 0 0 4.5 14H8l1 7h6l1-7h3.5A2.5 2.5 0 0 0 22 11.5V11a2 2 0 0 0-2-2z"/><path d="M12 3v6"/></svg>
            Open this link on your PC or laptop
          </div>
          <div class="mobile-tip">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"/></svg>
            Copy the URL and paste it in your browser
          </div>
        </div>
        <button class="mobile-overlay-dismiss" @click="dismissMobileOverlay">
          Continue anyway
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"/></svg>
        </button>
      </div>
    </div>
    <!-- ═══════════════════════════ HEADER ═══════════════════════════ -->
    <header class="site-header">
      <a class="brand" href="#top" aria-label="NexBill POS home">
        <img class="brand-logo" src="/assets/logo.png" alt="NexBill Logo">
        <span>NexBill <span class="brand-pos">POS</span></span>
      </a>
      <nav class="top-nav" aria-label="Main navigation">
        <a href="#about">About</a>
        <a href="#screenshots">Previews</a>
        <a href="#reviews">Reviews</a>
        <a href="#requirements">Requirements</a>
        <a href="#install">Install</a>
        <a href="#faq">FAQ</a>
      </nav>
      <button 
        class="header-cta" 
        @click="triggerDownload"
        :disabled="downloadState === 'downloading'"
      >
        <span v-if="downloadState === 'idle'" style="display: inline-flex; align-items: center; gap: 6px;">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
          Download Free
        </span>
        <span v-else-if="downloadState === 'downloading'">Downloading {{ downloadProgress }}%</span>
        <span v-else-if="downloadState === 'completed'">Downloaded</span>
      </button>
    </header>

    <main class="app-container" id="top">
      <!-- ═══════════════════════════ STORE HERO ═══════════════════════════ -->
      <section class="store-hero">
        <!-- Ambient Glow Elements in the Background -->
        <div class="store-hero-bg-glows">
          <div class="glow glow-1"></div>
          <div class="glow glow-2"></div>
        </div>

        <div class="store-hero-content">
          <div class="store-hero-main">
            <!-- App Large Icon -->
            <div class="store-icon-container">
              <img class="store-app-icon" src="/assets/logo.png" alt="NexBill POS Icon">
            </div>

            <!-- App Metadata Details -->
            <div class="store-meta-info">
              <h1 class="store-title">NexBill POS</h1>
              <p class="store-dev">Nexurah Tech · Business & Finance</p>
              
              <div class="store-tags">
                <span class="badge badge-primary">Smart Checkout</span>
                <span class="badge">GST Invoice</span>
                <span class="badge">Inventory</span>
                <span class="badge">WhatsApp Share</span>
              </div>

              <!-- Rating & Download Counts summary (Play Store style) -->
              <div class="store-rating-summary">
                <div class="rating-cell">
                  <span class="rating-val">
                    4.9 
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" style="color: var(--accent-warning);"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
                  </span>
                  <span class="rating-lbl">Average Rating</span>
                </div>
                <div class="rating-divider"></div>
                <div class="rating-cell">
                  <span class="rating-val">10K+</span>
                  <span class="rating-lbl">Downloads</span>
                </div>
                <div class="rating-divider"></div>
                <div class="rating-cell">
                  <span class="rating-val">v1.0.0</span>
                  <span class="rating-lbl">Latest Version</span>
                </div>
                <div class="rating-divider"></div>
                <div class="rating-cell">
                  <span class="rating-val">E</span>
                  <span class="rating-lbl">Everyone</span>
                </div>
              </div>
            </div>
          </div>

          <!-- Action and Installer Block (Microsoft Store style) -->
          <div class="store-action-block">
            <button 
              class="btn-install" 
              @click="triggerDownload" 
              :disabled="downloadState === 'downloading'"
            >
              <svg v-if="downloadState === 'idle'" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
              <span v-if="downloadState === 'idle'">Install</span>
              <span v-else-if="downloadState === 'downloading'">Installing... {{ downloadProgress }}%</span>
              <span v-else-if="downloadState === 'completed'">Launch Setup</span>
            </button>

            <!-- Interactive Download Progress Bar -->
            <div v-if="downloadState === 'downloading'" style="width: 100%; height: 4px; background: rgba(14, 56, 53, 0.05); border-radius: 99px; overflow: hidden; margin-top: -4px;">
              <div :style="{ width: downloadProgress + '%' }" style="height: 100%; background: var(--primary-light); border-radius: 99px; transition: width 0.1s linear;"></div>
            </div>

            <!-- OS Detection Banner -->
            <div class="os-banner" :class="{ 'os-banner-error': !isWindowsOS }">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M0 3.449L9.75 2.1v9.451H0m10.949-9.602L24 0v11.4H10.949M0 12.6h9.75v9.451L0 20.699M10.949 12.6H24V24l-12.9-1.801"/></svg>
              <span>{{ osText }}</span>
            </div>

            <div class="action-meta">
              <span>Size: ~331 MB</span>
              <span>Version: 1.0.0</span>
            </div>
          </div>
        </div>
      </section>

      <!-- ═══════════════════════════ GALLERY / SCREENSHOTS ═══════════════════════════ -->
      <section class="gallery-section" id="screenshots">
        <h3>
          <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>
          See it in Action
        </h3>
        
        <div class="gallery-viewport-container">
          <!-- Prev Button -->
          <button class="gallery-nav-btn prev" @click="scrollGallery(-1)" aria-label="Previous screenshots">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="15 18 9 12 15 6"/></svg>
          </button>
          
          <!-- Viewport -->
          <div class="gallery-viewport" ref="galleryViewport">
            <div 
              v-for="(img, idx) in screenshots" 
              :key="idx" 
              class="gallery-slide"
              @click="openLightbox(idx)"
            >
              <img 
                :src="img.src" 
                :alt="img.title" 
                class="gallery-image"
                loading="lazy"
              >
              <div class="gallery-slide-info" style="position: absolute; bottom: 0; left: 0; right: 0; padding: 16px; background: linear-gradient(to top, rgba(14, 56, 53, 0.95), transparent); z-index: 2;">
                <h4 style="font-size: 1rem; color: #fff;">{{ img.title }}</h4>
                <p style="font-size: 0.8rem; color: #cbd5e1; margin-top: 4px;">{{ img.desc }}</p>
              </div>
            </div>
          </div>
          
          <!-- Next Button -->
          <button class="gallery-nav-btn next" @click="scrollGallery(1)" aria-label="Next screenshots">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"/></svg>
          </button>
        </div>
      </section>

      <!-- ═══════════════════════════ LIGHTBOX MODAL ═══════════════════════════ -->
      <div v-if="lightbox.open" class="lightbox-modal" @click="closeLightbox">
        <button class="lightbox-close" @click.stop="closeLightbox">✕</button>
        
        <!-- Lightbox Gallery Controls -->
        <button class="gallery-nav-btn prev" style="left: 20px;" @click.stop="prevLightboxImage">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="15 18 9 12 15 6"/></svg>
        </button>

        <div class="lightbox-content" @click.stop>
          <img :src="screenshots[lightbox.activeIndex].src" :alt="screenshots[lightbox.activeIndex].title" class="lightbox-image">
          <div class="lightbox-caption">
            <h3>{{ screenshots[lightbox.activeIndex].title }}</h3>
            <p>{{ screenshots[lightbox.activeIndex].desc }}</p>
          </div>
        </div>

        <button class="gallery-nav-btn next" style="right: 20px;" @click.stop="nextLightboxImage">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"/></svg>
        </button>
      </div>

      <!-- ═══════════════════════════ MAIN DETAILS GRID ═══════════════════════════ -->
      <section class="details-grid">
        <!-- Left details: Overview, Features, Reviews, Requirements -->
        <div class="details-left">
          
          <!-- App Description / Overview -->
          <div class="detail-card" id="about">
            <h2>Description</h2>
            <div style="color: var(--text-secondary); line-height: 1.7;">
              <p :style="{ display: showMoreDesc ? 'block' : '-webkit-box', '-webkit-line-clamp': showMoreDesc ? 'none' : '3', '-webkit-box-orient': 'vertical', overflow: 'hidden' }">
                NexBill POS is a high-speed, billing and customer management desktop application engineered specifically for Indian retail stores. Whether you operate a grocery outlet, apparel boutique, electrical store, or supermarket, NexBill POS converts your Windows desktop into an advanced billing terminal. Scan product barcodes, compute GST taxes automatically, record customer databases, track credit accounts, and send invoices instantly to your clients' WhatsApp profiles. No complex commands or server setups required—it works seamlessly.
              </p>
              <button 
                @click="showMoreDesc = !showMoreDesc" 
                style="background: none; border: none; color: var(--primary-light); font-weight: 700; font-size: 0.9rem; margin-top: 10px; cursor: pointer; display: flex; align-items: center; gap: 4px;"
              >
                <span>{{ showMoreDesc ? 'Read less' : 'Read more' }}</span>
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" :style="{ transform: showMoreDesc ? 'rotate(180deg)' : 'none', transition: 'transform 0.2s' }"><polyline points="6 9 12 15 18 9"/></svg>
              </button>
            </div>
          </div>

          <!-- Feature Grid -->
          <div class="detail-card">
            <h2>Key Features</h2>
            <div class="features-grid">
              <div v-for="(feat, idx) in features" :key="idx" class="feat-item-new">
                <div class="feat-icon-new">
                  <!-- Render feature SVGs -->
                  <svg v-if="feat.id === 'checkout'" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/></svg>
                  <svg v-else-if="feat.id === 'stock'" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg>
                  <svg v-else-if="feat.id === 'gst'" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/><polyline points="10 9 9 9 8 9"/></svg>
                  <svg v-else-if="feat.id === 'whatsapp'" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="5" y="2" width="14" height="20" rx="2" ry="2"/><line x1="12" y1="18" x2="12.01" y2="18"/></svg>
                  <svg v-else-if="feat.id === 'reports'" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg>
                  <svg v-else-if="feat.id === 'cloud'" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><ellipse cx="12" cy="5" rx="9" ry="3"/><path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"/><path d="M3 12c0 1.66 4 3 9 3s9-1.34 9-3"/></svg>
                </div>
                <div class="feat-copy-new">
                  <h4>{{ feat.title }}</h4>
                  <p>{{ feat.desc }}</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Ratings & Reviews -->
          <div class="detail-card" id="reviews">
            <h2>Ratings & Reviews</h2>
            
            <div class="reviews-summary">
              <div class="rating-total-card">
                <div class="big-rating">{{ computedAverageRating }}</div>
                <div class="big-rating-stars">
                  <!-- Vector star icons instead of characters -->
                  <svg v-for="star in 5" :key="star" width="16" height="16" viewBox="0 0 24 24" fill="currentColor" style="color: var(--accent-warning); margin: 0 1px;"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
                </div>
                <div class="rating-count-label">Based on {{ reviewsList.length }} Ratings</div>
              </div>

              <!-- Rating breakdown bars -->
              <div class="rating-bars-container">
                <div v-for="stars in [5, 4, 3, 2, 1]" :key="stars" class="rating-bar-row">
                  <span class="star-num">{{ stars }}</span>
                  <svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor" style="color: var(--accent-warning);"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
                  <div class="rating-bar-track">
                    <div class="rating-bar-fill" :style="{ width: getStarPercentage(stars) + '%' }"></div>
                  </div>
                  <span class="review-percentage">{{ getStarCount(stars) }}</span>
                </div>
              </div>
            </div>

            <!-- Review filters and actions -->
            <div class="reviews-actions">
              <div class="reviews-filters">
                <button 
                  class="filter-btn" 
                  :class="{ active: activeReviewFilter === 'all' }"
                  @click="activeReviewFilter = 'all'"
                >
                  All ({{ reviewsList.length }})
                </button>
                <button 
                  v-for="stars in [5, 4, 3, 2, 1]" 
                  :key="stars"
                  class="filter-btn"
                  :class="{ active: activeReviewFilter === stars }"
                  @click="activeReviewFilter = stars"
                >
                  {{ stars }} ★ ({{ getStarCount(stars) }})
                </button>
              </div>

              <input 
                v-model="reviewSearchQuery" 
                type="text" 
                class="review-search" 
                placeholder="Search reviews..."
              >
            </div>

            <!-- Reviews list -->
            <div class="reviews-list">
              <div 
                v-for="(rev, idx) in filteredReviews" 
                :key="idx" 
                class="review-card"
              >
                <div class="review-header">
                  <div class="review-author-group">
                    <div class="avatar-mock">{{ rev.author.charAt(0) }}</div>
                    <div class="author-meta">
                      <span class="author-name">{{ rev.author }}</span>
                      <span class="review-date">{{ rev.date }}</span>
                    </div>
                  </div>
                  <div class="review-stars">
                    <!-- Vector star graphics loop -->
                    <svg v-for="star in rev.stars" :key="star" width="14" height="14" viewBox="0 0 24 24" fill="currentColor" style="color: var(--accent-warning); display: inline-block; margin-right: 1px;"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
                    <svg v-for="star in (5 - rev.stars)" :key="star + 'empty'" width="14" height="14" viewBox="0 0 24 24" fill="currentColor" style="color: #e2e8f0; display: inline-block; margin-right: 1px;"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
                  </div>
                </div>
                <div class="review-body">
                  <h4>{{ rev.title }}</h4>
                  <p>{{ rev.content }}</p>
                </div>
              </div>

              <div v-if="filteredReviews.length === 0" style="text-align: center; padding: 40px; color: var(--text-muted);">
                No reviews found matching your filters.
              </div>
            </div>

            <!-- Mock Review Submission Form -->
            <div class="write-review-widget">
              <h3>Write a Review</h3>
              <div class="rating-select-row">
                <span style="font-size: 0.95rem; font-weight: 700; color: var(--text-secondary);">Your Rating:</span>
                <div style="display: flex; gap: 6px;">
                  <!-- Interactive stars with vector SVG paths -->
                  <svg 
                    v-for="star in 5" 
                    :key="star" 
                    width="24" height="24" 
                    viewBox="0 0 24 24" 
                    fill="currentColor"
                    class="star-interactive"
                    :class="{ active: newReview.stars >= star }"
                    @click="newReview.stars = star"
                    style="margin-right: 2px;"
                  >
                    <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>
                  </svg>
                </div>
              </div>

              <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 16px;">
                <div class="form-group">
                  <label for="rev-name">Your Name</label>
                  <input id="rev-name" v-model="newReview.name" type="text" class="review-input" placeholder="e.g. Anand Kumar">
                </div>
                <div class="form-group">
                  <label for="rev-title">Review Title</label>
                  <input id="rev-title" v-model="newReview.title" type="text" class="review-input" placeholder="e.g. Extremely Fast checkout!">
                </div>
              </div>

              <div class="form-group">
                <label for="rev-content">Review Details</label>
                <textarea id="rev-content" v-model="newReview.content" rows="4" class="review-input" placeholder="Tell us your experience using NexBill POS..."></textarea>
              </div>

              <button class="btn-install" style="width: auto; padding: 12px 28px; margin-top: 10px;" @click="submitMockReview">
                Submit Review
              </button>
            </div>
          </div>

          <!-- System Requirements -->
          <div class="detail-card" id="requirements">
            <h2>System Requirements</h2>
            
            <div class="tabs-header">
              <button 
                class="tab-trigger" 
                :class="{ active: reqTab === 'minimum' }"
                @click="reqTab = 'minimum'"
              >
                Minimum Requirements
              </button>
              <button 
                class="tab-trigger" 
                :class="{ active: reqTab === 'recommended' }"
                @click="reqTab = 'recommended'"
              >
                Recommended Setup
              </button>
            </div>

            <div class="tabs-content">
              <table v-if="reqTab === 'minimum'" class="reqs-table">
                <tbody>
                  <tr>
                    <td class="req-label">OS</td>
                    <td class="req-value">Windows 10 (64-bit Version 1909 or higher)</td>
                  </tr>
                  <tr>
                    <td class="req-label">Processor</td>
                    <td class="req-value">Intel Core i3 or AMD Ryzen 3 (Dual Core, 2.0 GHz)</td>
                  </tr>
                  <tr>
                    <td class="req-label">Memory (RAM)</td>
                    <td class="req-value">4 GB RAM</td>
                  </tr>
                  <tr>
                    <td class="req-label">Graphics</td>
                    <td class="req-value">DirectX 11 compatible integrated graphics</td>
                  </tr>
                  <tr>
                    <td class="req-label">Storage Space</td>
                    <td class="req-value">200 MB free space (SSD recommended for databases)</td>
                  </tr>
                  <tr>
                    <td class="req-label">Internet</td>
                    <td class="req-value">Active internet connection (for cloud sync & WhatsApp sharing)</td>
                  </tr>
                </tbody>
              </table>

              <table v-if="reqTab === 'recommended'" class="reqs-table">
                <tbody>
                  <tr>
                    <td class="req-label">OS</td>
                    <td class="req-value">Windows 11 (64-bit)</td>
                  </tr>
                  <tr>
                    <td class="req-label">Processor</td>
                    <td class="req-value">Intel Core i5 or AMD Ryzen 5 (Quad Core, 2.8 GHz or higher)</td>
                  </tr>
                  <tr>
                    <td class="req-label">Memory (RAM)</td>
                    <td class="req-value">8 GB RAM or more</td>
                  </tr>
                  <tr>
                    <td class="req-label">Graphics</td>
                    <td class="req-value">Intel Iris Xe / AMD Radeon Vega or dedicated GPU</td>
                  </tr>
                  <tr>
                    <td class="req-label">Storage Space</td>
                    <td class="req-value">500 MB free space on SSD</td>
                  </tr>
                  <tr>
                    <td class="req-label">Internet</td>
                    <td class="req-value">Stable Broadband connection (Fibre/LTE)</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <!-- Right details: App Metadata sidebar -->
        <div class="details-sidebar">
          
          <!-- Additional Info Sidebar (Microsoft Store Style) -->
          <div class="sidebar-block">
            <h3>Additional Information</h3>
            <div class="meta-table-list">
              <div class="meta-table-row">
                <span class="meta-label">Published by</span>
                <span class="meta-val">Nexurah Tech</span>
              </div>
              <div class="meta-table-row">
                <span class="meta-label">Release Date</span>
                <span class="meta-val">June 10, 2026</span>
              </div>
              <div class="meta-table-row">
                <span class="meta-label">Installation size</span>
                <span class="meta-val">331.4 MB</span>
              </div>
              <div class="meta-table-row">
                <span class="meta-label">Architecture</span>
                <span class="meta-val">Windows x64 (64-bit)</span>
              </div>
              <div class="meta-table-row">
                <span class="meta-label">Category</span>
                <span class="meta-val">POS, Invoicing, Inventory</span>
              </div>
              <div class="meta-table-row">
                <span class="meta-label">Database Sync</span>
                <span class="meta-val green">Cloud (MongoDB Enabled)</span>
              </div>
              <div class="meta-table-row">
                <span class="meta-label">Pricing</span>
                <span class="meta-val">Free trial (Subscription after trial)</span>
              </div>
            </div>
          </div>

          <!-- Quick Support Sidebar Info -->
          <div class="sidebar-block">
            <h3>Customer Support</h3>
            <p style="font-size: 0.88rem; color: var(--text-secondary); margin-bottom: 20px;">
              Need help installing NexBill POS or setting up your product list? Contact our team anytime.
            </p>
            <div class="support-cards-list">
              <a href="https://wa.me/919600950190" target="_blank" rel="noopener" class="support-card-new">
                <div class="support-icon whatsapp">
                  <!-- SVG Chat bubble icon instead of emoji -->
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
                </div>
                <div class="support-copy">
                  <strong>WhatsApp Support</strong>
                  <span>+91 96009 50190</span>
                  <em>Replies in 5-10 minutes</em>
                </div>
              </a>

              <a href="mailto:support@nexbill.com" class="support-card-new">
                <div class="support-icon email">
                  <!-- SVG Mail Envelope icon instead of emoji -->
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
                </div>
                <div class="support-copy">
                  <strong>Email Support</strong>
                  <span>support@nexbill.com</span>
                  <em>Response in 24 hours</em>
                </div>
              </a>
            </div>
          </div>
        </div>
      </section>

      <!-- ═══════════════════════════ INSTALL STEPS (Microsoft Store Flow) ═══════════════════════════ -->
      <section class="install-section" id="install">
        <div class="install-section-head">
          <p class="eyebrow">Visual Flow</p>
          <h2>How to Install NexBill POS</h2>
          <p>Four quick steps to configure the application on your computer.</p>
        </div>

        <div class="install-steps-flex">
          <div class="install-step-card">
            <div class="watermark-num">01</div>
            <div class="install-step-icon">
              <!-- SVG Downward Circle Arrow instead of emoji -->
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="8 12 12 16 16 12"/><line x1="12" y1="8" x2="12" y2="16"/></svg>
            </div>
            <span class="step-badge">Step 1</span>
            <h3>Download Setup</h3>
            <p>Click the <strong>Install</strong> button above to download the <strong>NexBilling.Setup.exe</strong> installer file.</p>
          </div>
          <div class="install-step-card">
            <div class="watermark-num">02</div>
            <div class="install-step-icon">
              <!-- SVG Package instead of emoji -->
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg>
            </div>
            <span class="step-badge">Step 2</span>
            <h3>Launch Installer</h3>
            <p>Open your download directory and double-click the file to start the installation wizard.</p>
          </div>
          <div class="install-step-card">
            <div class="watermark-num">03</div>
            <div class="install-step-icon">
              <!-- SVG Shield Warning instead of emoji -->
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/></svg>
            </div>
            <span class="step-badge">Step 3</span>
            <h3>Bypass SmartScreen</h3>
            <p>If Windows blocks it, click <strong>"More Info"</strong> then <strong>"Run Anyway"</strong>. The setup is safe.</p>
          </div>
          <div class="install-step-card">
            <div class="watermark-num">04</div>
            <div class="install-step-icon">
              <!-- SVG Check Success instead of emoji -->
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>
            </div>
            <span class="step-badge">Step 4</span>
            <h3>Login & Bill</h3>
            <p>Enter your shop profile credentials and start scanning items to print receipts instantly.</p>
          </div>
        </div>
      </section>

      <!-- ═══════════════════════════ FAQ SECTION (Interactive Search) ═══════════════════════════ -->
      <section class="detail-card" id="faq" style="margin-bottom: 60px;">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 28px; flex-wrap: wrap; gap: 16px;">
          <h2>Frequently Asked Questions</h2>
          <input 
            v-model="faqSearchQuery" 
            type="text" 
            class="review-search" 
            placeholder="Search FAQs..."
            style="min-width: 280px;"
          >
        </div>

        <div class="faq-grid">
          <div 
            v-for="(faq, idx) in filteredFAQs" 
            :key="idx" 
            class="faq-item-custom"
            :class="{ open: faq.open }"
          >
            <button class="faq-trigger" @click="faq.open = !faq.open">
              <span>{{ faq.q }}</span>
              <span class="faq-chevron">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 12 15 18 9"/></svg>
              </span>
            </button>
            <div v-if="faq.open" class="faq-content">
              <p>{{ faq.a }}</p>
            </div>
          </div>

          <div v-if="filteredFAQs.length === 0" style="text-align: center; padding: 40px; color: var(--text-muted);">
            No matching FAQs found.
          </div>
        </div>
      </section>
    </main>

    <!-- ═══════════════════════════ FOOTER ═══════════════════════════ -->
    <footer class="site-footer">
      <div class="app-container">
        <div class="footer-brand">
          <img src="/assets/logo.png" alt="NexBill Logo" class="footer-logo">
          <span>NexBill POS</span>
        </div>
        <p class="footer-tagline">Smart Billing and Inventory for Indian Retail Shops</p>
        <p class="footer-copy">© 2026 Nexurah Tech. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      // Mobile detection
      isMobile: false,

      // Installer state: 'idle', 'downloading', 'completed'
      downloadState: 'idle',
      downloadProgress: 0,
      downloadTimer: null,
      downloadUrl: 'https://github.com/nexurah-tech/billing-customer-app/releases/download/v0.1.0/NexBilling.Setup.0.1.0.exe',
      
      // OS Detection
      isWindowsOS: true,
      osText: 'Checking Compatibility...',

      // Description accordion
      showMoreDesc: false,

      // Screenshot items
      screenshots: [
        {
          src: '/assets/screenshots/screenshot_dashboard.png',
          title: 'Smart POS Terminal',
          desc: 'Quickly scan barcodes, add items to cart, apply discounts, select payment mode, and checkout in seconds.'
        },
        {
          src: '/assets/screenshots/screenshot_invoices.png',
          title: 'Invoices & Billing History',
          desc: 'Browse history, filter by date, print dual formats, check unpaid credits, and share directly via WhatsApp.'
        },
        {
          src: '/assets/screenshots/Screenshot 2026-06-10 190052.png',
          title: 'Dynamic Product Catalog',
          desc: 'Add individual products, set prices, track stock levels, and import inventory lists in bulk using Excel templates.'
        },
        {
          src: '/assets/screenshots/Screenshot 2026-06-10 190449.png',
          title: 'Customer Directory',
          desc: 'Keep track of customer details, billing history, outstanding credit balances, and loyalty profiles.'
        },
        {
          src: '/assets/screenshots/Screenshot 2026-06-10 190904.png',
          title: 'GST & Sales Analytics',
          desc: 'Review gross sales, net profit margins, daily totals, and generate tax audit logs automatically.'
        },
        {
          src: '/assets/screenshots/Screenshot 2026-06-10 191104.png',
          title: 'Thermal Printer Integration',
          desc: 'Configure paper size settings, connect thermal POS receipt printers, and customize headers and footers.'
        },
        {
          src: '/assets/screenshots/login asset.png',
          title: 'Secure Account Authentication',
          desc: 'Log in with encrypted user credentials, manage role permissions, and sync your shop data securely.'
        },
        {
          src: '/assets/screenshots/nexbill-desktop-preview.png',
          title: 'Polished Desktop Terminal',
          desc: 'Offline-first native desktop terminal optimized for fast navigation and keyboard shortcuts.'
        },
        {
          src: '/assets/screenshots/Screenshot 2026-05-31 130636.png',
          title: 'Easy Initial Setup',
          desc: 'Set up shop details, currency signs, barcode scan triggers, and custom settings to get started instantly.'
        }
      ],

      // Lightbox state
      lightbox: {
        open: false,
        activeIndex: 0
      },

      // Key Features
      features: [
        {
          id: 'checkout',
          title: 'Ultra-fast checkout',
          desc: 'Scan barcodes or type shortcuts to complete invoices. Print or WhatsApp them in seconds.'
        },
        {
          id: 'stock',
          title: 'Real-time Stock Monitor',
          desc: 'Track physical inventory levels, receive automatic low-stock notifications, and bulk import items.'
        },
        {
          id: 'gst',
          title: 'GST Compliant Taxes',
          desc: 'Automatically computes CGST, SGST, and IGST components for retail and wholesaling.'
        },
        {
          id: 'whatsapp',
          title: 'Direct WhatsApp Share',
          desc: 'Send digital PDF receipts straight to your client\'s mobile phone number without print cost.'
        },
        {
          id: 'reports',
          title: 'Sales Reports & Analytics',
          desc: 'Review daily revenue trends, item-wise profit, and customer accounts reports instantly.'
        },
        {
          id: 'cloud',
          title: 'Cloud Sync Architecture',
          desc: 'Keep shop records backed up securely in the cloud. Access POS databases anywhere on multiple setups.'
        }
      ],

      // System Requirements Tab: 'minimum' | 'recommended'
      reqTab: 'minimum',

      // Ratings & Reviews Database
      reviewsList: [
        {
          author: 'Anand K. (Grocery Store Owner)',
          stars: 5,
          date: 'Yesterday',
          title: 'Saves hours of manual register entries!',
          content: 'I have been using NexBill POS for my grocery store for the last 3 weeks. Setting up products from Excel was extremely easy, and generating GST receipts takes just seconds. Highly recommend the WhatsApp share feature—it saves on paper costs!'
        },
        {
          author: 'Sushma Sen (Boutique Designer)',
          stars: 5,
          date: '3 days ago',
          title: 'Beautiful modern design & very fast',
          content: 'Most retail billing software looks like it was designed in the 90s. NexBill is beautiful and clean. Setup was simple on my Windows 11 laptop, and training my cashier staff took less than 10 minutes.'
        },
        {
          author: 'Vikram Mehta (Electrical Hardware)',
          stars: 4,
          date: '1 week ago',
          title: 'Great offline features, good WhatsApp sync',
          content: 'Very happy with the invoice generator. The barcode scan has had zero delays. I wish there was a way to customize thermal receipt sizes a bit more, but otherwise it works exactly as promised!'
        },
        {
          author: 'Deepak Raj (Supermarket)',
          stars: 5,
          date: '2 weeks ago',
          title: 'Solid inventory control tracking',
          content: 'My inventory levels are finally accurate. The system triggers warnings when items run low. Cloud syncing works well when switching billing computers.'
        }
      ],
      activeReviewFilter: 'all', // 'all' or 1,2,3,4,5
      reviewSearchQuery: '',

      // Write review form data
      newReview: {
        stars: 5,
        name: '',
        title: '',
        content: ''
      },

      // FAQ database
      faqs: [
        {
          q: 'Is NexBill POS free to download?',
          a: 'Yes! NexBill POS is completely free to download and comes with a 14-day trial period. A subscription is required after the trial to continue syncing database information securely with the cloud.',
          open: true
        },
        {
          q: 'Is NexBill POS GST compliant?',
          a: 'Yes, fully. NexBill POS automatically calculates CGST, SGST, and IGST based on product settings and outputs compliant tax invoices ready for account filing.',
          open: false
        },
        {
          q: 'Can I share invoices on WhatsApp?',
          a: 'Yes! After creating a bill, you can click the WhatsApp button to send a PDF copy or receipt web link directly to the customer\'s mobile number.',
          open: false
        },
        {
          q: 'What if Windows SmartScreen blocks installation?',
          a: 'This is a standard warning for newly published Windows applications. When the SmartScreen prompt displays, click on "More Info" and then click "Run Anyway". The application contains no malware and is fully secure.',
          open: false
        },
        {
          q: 'Does it work offline?',
          a: 'Yes, core billing processes work offline. However, cloud syncing and WhatsApp receipt sharing require a stable internet connection.',
          open: false
        },
        {
          q: 'Can multiple computers share the same store data?',
          a: 'Yes. NexBill POS supports multi-user login. You can install the client on multiple computers in your store, and all of them will read/write from your secure cloud database in real-time.',
          open: false
        }
      ],
      faqSearchQuery: ''
    };
  },
  computed: {
    computedAverageRating() {
      if (this.reviewsList.length === 0) return 0;
      const sum = this.reviewsList.reduce((acc, curr) => acc + curr.stars, 0);
      return (sum / this.reviewsList.length).toFixed(1);
    },
    filteredReviews() {
      let result = this.reviewsList;
      
      // Filter by stars
      if (this.activeReviewFilter !== 'all') {
        result = result.filter(r => r.stars === this.activeReviewFilter);
      }
      
      // Filter by search query
      if (this.reviewSearchQuery.trim()) {
        const q = this.reviewSearchQuery.toLowerCase();
        result = result.filter(r => 
          r.title.toLowerCase().includes(q) || 
          r.content.toLowerCase().includes(q) || 
          r.author.toLowerCase().includes(q)
        );
      }
      
      return result;
    },
    filteredFAQs() {
      if (!this.faqSearchQuery.trim()) return this.faqs;
      const q = this.faqSearchQuery.toLowerCase();
      return this.faqs.filter(f => 
        f.q.toLowerCase().includes(q) || 
        f.a.toLowerCase().includes(q)
      );
    }
  },
  mounted() {
    this.detectOS();
    this.detectMobile();
    // Register scroll and arrow keys event listener for lightbox
    window.addEventListener('keydown', this.handleKeyDown);
  },
  beforeUnmount() {
    window.removeEventListener('keydown', this.handleKeyDown);
    if (this.downloadTimer) clearInterval(this.downloadTimer);
  },
  methods: {
    detectMobile() {
      const ua = window.navigator?.userAgent || '';
      const isMobileUA = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(ua);
      const isNarrowScreen = window.innerWidth <= 768;
      this.isMobile = isMobileUA || isNarrowScreen;
    },
    dismissMobileOverlay() {
      this.isMobile = false;
    },
    detectOS() {
      const platform = window.navigator?.userAgent || '';
      if (platform.includes('Windows') || platform.includes('Win')) {
        this.isWindowsOS = true;
        this.osText = 'Compatible with Windows 10 & 11 (64-bit)';
      } else {
        this.isWindowsOS = false;
        this.osText = 'Compatible with Windows 10 & 11 only';
      }
    },
    triggerDownload() {
      if (this.downloadState === 'downloading') return;
      
      // Trigger actual file download
      const link = document.createElement('a');
      link.href = this.downloadUrl;
      link.setAttribute('download', 'NexBilling.Setup.0.1.0.exe');
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);

      // Simulate download progress
      this.downloadState = 'downloading';
      this.downloadProgress = 0;
      
      this.downloadTimer = setInterval(() => {
        if (this.downloadProgress < 100) {
          // Increment progress
          this.downloadProgress += Math.floor(Math.random() * 8) + 2;
          if (this.downloadProgress > 100) this.downloadProgress = 100;
        } else {
          clearInterval(this.downloadTimer);
          this.downloadTimer = null;
          this.downloadState = 'completed';
          
          // Revert back to idle install after a few seconds so they can install again if needed
          setTimeout(() => {
            this.downloadState = 'idle';
          }, 8000);
        }
      }, 150);
    },
    openWhatsAppSupport() {
      window.open('https://wa.me/919600950190?text=Hi,%20I%27d%20like%20to%20get%20a%20demo%20of%20NexBill%20POS.', '_blank');
    },
    scrollGallery(direction) {
      const el = this.$refs.galleryViewport;
      if (!el) return;
      const scrollAmt = 500; // Scroll increment
      el.scrollBy({
        left: scrollAmt * direction,
        behavior: 'smooth'
      });
    },
    // Lightbox methods
    openLightbox(index) {
      this.lightbox.activeIndex = index;
      this.lightbox.open = true;
      document.body.style.overflow = 'hidden'; // Lock scrolling
    },
    closeLightbox() {
      this.lightbox.open = false;
      document.body.style.overflow = ''; // Unlock scrolling
    },
    prevLightboxImage() {
      if (this.lightbox.activeIndex > 0) {
        this.lightbox.activeIndex--;
      } else {
        this.lightbox.activeIndex = this.screenshots.length - 1;
      }
    },
    nextLightboxImage() {
      if (this.lightbox.activeIndex < this.screenshots.length - 1) {
        this.lightbox.activeIndex++;
      } else {
        this.lightbox.activeIndex = 0;
      }
    },
    handleKeyDown(e) {
      if (!this.lightbox.open) return;
      if (e.key === 'Escape') this.closeLightbox();
      if (e.key === 'ArrowRight') this.nextLightboxImage();
      if (e.key === 'ArrowLeft') this.prevLightboxImage();
    },
    // Ratings & Reviews helpers
    getStarCount(stars) {
      return this.reviewsList.filter(r => r.stars === stars).length;
    },
    getStarPercentage(stars) {
      if (this.reviewsList.length === 0) return 0;
      return (this.getStarCount(stars) / this.reviewsList.length) * 100;
    },
    submitMockReview() {
      // Validate
      if (!this.newReview.name.trim() || !this.newReview.title.trim() || !this.newReview.content.trim()) {
        alert('Please fill out all fields before submitting.');
        return;
      }

      // Add to reviews database
      this.reviewsList.unshift({
        author: this.newReview.name + ' (Verified User)',
        stars: this.newReview.stars,
        date: 'Just now',
        title: this.newReview.title,
        content: this.newReview.content
      });

      // Clear form
      this.newReview.name = '';
      this.newReview.title = '';
      this.newReview.content = '';
      this.newReview.stars = 5;

      alert('Thank you! Your review has been successfully submitted and added.');
    }
  }
};
</script>

<style scoped>
.app-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* ── Mobile Device Overlay ───────────────────────────────── */
.mobile-overlay {
  position: fixed;
  inset: 0;
  z-index: 9999;
  background: linear-gradient(145deg, #f0faf8 0%, #e6f7f4 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
}

.mobile-overlay-card {
  background: #ffffff;
  border: 1px solid rgba(14, 56, 53, 0.08);
  border-radius: 24px;
  padding: 44px 32px;
  max-width: 400px;
  width: 100%;
  text-align: center;
  box-shadow: 0 24px 64px -12px rgba(14, 56, 53, 0.12), 0 0 0 1px rgba(20, 184, 166, 0.06);
}

.mobile-overlay-icon {
  width: 88px;
  height: 88px;
  background: linear-gradient(135deg, rgba(20, 184, 166, 0.1) 0%, rgba(20, 184, 166, 0.03) 100%);
  border: 1px solid rgba(20, 184, 166, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 24px;
  color: #14b8a6;
}

.mobile-overlay-title {
  font-family: 'Outfit', 'Inter', sans-serif;
  font-size: 1.75rem;
  font-weight: 800;
  color: #0e3835;
  margin-bottom: 14px;
  letter-spacing: -0.02em;
}

.mobile-overlay-desc {
  font-size: 0.95rem;
  color: #475569;
  line-height: 1.65;
  margin-bottom: 28px;
}

.mobile-overlay-tips {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-bottom: 32px;
  text-align: left;
}

.mobile-tip {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.85rem;
  font-weight: 600;
  color: #0e3835;
  background: rgba(20, 184, 166, 0.05);
  border: 1px solid rgba(20, 184, 166, 0.1);
  border-radius: 10px;
  padding: 12px 16px;
}

.mobile-tip svg {
  flex-shrink: 0;
  color: #14b8a6;
}

.mobile-overlay-dismiss {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  background: none;
  border: none;
  color: #64748b;
  font-size: 0.82rem;
  font-weight: 600;
  cursor: pointer;
  padding: 8px 12px;
  border-radius: 8px;
  transition: color 0.2s, background 0.2s;
}

.mobile-overlay-dismiss:hover {
  color: #0e3835;
  background: rgba(14, 56, 53, 0.04);
}
</style>
