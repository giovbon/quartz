---
title: Tailwind
tags:
  - frontend
---
![[JavaScript#^LinksJavascript]]

# Tailwind

* Textos
	* Tamanho de fontes
		* ​`text-xs`​ — Extra pequeno (0.75rem)
		* ​`text-sm`​ — Pequeno (0.875rem)
		* ​`text-base`​ — Base/padrão (1rem)
		* ​`text-lg`​ — Grande (1.125rem)
		* ​`text-xl`​ — Extra grande (1.25rem)
		* ​`text-2xl`​ — 2x Extra grande (1.5rem)
		* ​`text-3xl`​ — 3x Extra grande (1.875rem)
		* ​`text-4xl`​ — 4x Extra grande (2.25rem)
		* ​`text-5xl`​ — 5x Extra grande (3rem)
		* ​`text-6xl`​ — 6x Extra grande (3.75rem)
		* ​`text-7xl`​ — 7x Extra grande (4.5rem)
		* ​`text-8xl`​ — 8x Extra grande (6rem)
		* ​`text-9xl`​ — 9x Extra grande (8rem)
	* Cores de fontes
		* ​**​`text-{color}`​** ​: Para cores pré-definidas, como `text-red-500`​, `text-blue-400`​, etc.
		* ​**​`text-{customColor}`​** ​: Para cores personalizadas definidas no arquivo `tailwind.config.js`​, como `text-nord5`​.

* Mobile First e Classes responsivas
	* O Tailwind segue o princípio do **mobile-first**, o que significa que as classes de estilo básicas (sem modificadores de breakpoint) são aplicadas a telas menores e, em seguida, você usa os breakpoints para alterar ou adicionar estilos para telas maiores.
	* ​**​`sm:`​** ​ — Para telas  **≥ 640px** (geralmente, dispositivos móveis)
	* ​**​`md:`​** ​ — Para telas  **≥ 768px** (geralmente, tablets)
	* ​**​`lg:`​** ​ — Para telas  **≥ 1024px** (geralmente, desktops pequenos)
	* ​**​`xl:`​** ​ — Para telas  **≥ 1280px** (geralmente, desktops grandes)
	* ​**​`2xl:`​** ​ — Para telas  **≥ 1536px** (geralmente, telas extra grandes)

* Margin `m`​ e padding `p`​
	* Seguem o padrão de, por exemplo em margin (serve para padding apenas mudando para `p`​): seguem o formato `m`​ para margem geral, `mt`​ (top) para margem superior, `mb`​ (botton) para margem inferior, `ml`​ (left) para margem à esquerda e `mr`​ (right) para margem à direita. `mx`​ aplica margin apenas aos lados esquerdo e direito do elemento e `my`​ aplica aos lados superior e inferior. Segue-se de `-`​ mais o numero:
	* ​**​`m-1`​**​: 0.25rem (4px)
	* ​**​`m-2`​**​: 0.5rem (8px)
	* ​**​`m-3`​**​: 0.75rem (12px)
	* ​**​`m-4`​**​: 1rem (16px)
	* ​**​`m-5`​**​: 1.25rem (20px)
	* ​**​`m-6`​**​: 1.5rem (24px)
	* ​**​`m-8`​**​: 2rem (32px)
	* ​**​`m-10`​**​: 2.5rem (40px)
	* ​**​`m-12`​**​: 3rem (48px)
	* ​**​`m-16`​**​: 4rem (64px)