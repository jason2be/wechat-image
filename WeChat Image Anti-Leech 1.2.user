// ==UserScript==
// @name         微信图片防盗链破解
// @namespace    http://tampermonkey.net/
// @version      1.2
// @description  强制绕过微信图片防盗链限制
// @author       @Jason2be
// @match        *://*/*
// @run-at       document-start
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // 核心策略1: 全局禁止发送Referer
    const meta = document.createElement('meta');
    meta.name = 'referrer';
    meta.content = 'no-referrer';
    document.head.appendChild(meta);

    // 核心策略2: 动态修复已加载的图片
    const fixWechatImages = () => {
        document.querySelectorAll('img[src*="mmbiz.qpic.cn"]').forEach(img => {
            if (img.src.includes('wx_co=1')) { // 替换过期参数
                img.src = img.src.replace('wx_co=1', 'wx_co=0') + '&_t=' + Date.now();
            }
            img.referrerPolicy = 'no-referrer'; // 双重保险
        });
    };

    // 首次执行
    fixWechatImages();

    // 监听动态加载内容
    new MutationObserver(fixWechatImages).observe(
        document.body,
        { childList: true, subtree: true }
    );
})();
