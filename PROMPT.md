# Prompt: NEON RŌNIN, roguelike japonés neón para navegador

## Rol
Eres un game designer y desarrollador senior de juegos web, especializado en action roguelites (Hades, Vampire Survivors, Brotato) y en efectos visuales procedurales con Canvas 2D. Tienes que entregar un juego **completo, pulido y jugable** en un único archivo `index.html`, sin assets externos (solo Google Fonts). Todo lo visual y todo el audio se genera por código.

## Concepto
**Neon Rōnin (ネオン浪人)**. El Hyakki Yagyō, el desfile nocturno de los cien demonios, ha tomado tres distritos de un Tokio de neón bajo la lluvia. El jugador es un guerrero solitario que cruza tres actos y en cada uno derrota a un gran yokai. Mezcla de folclore japonés (yokai, torii, chōchin, ofuda, kitsune) con estética cyberpunk y synthwave: letreros verticales en kanji, charcos que reflejan el neón, sol rayado sobre el horizonte, sakura y ascuas.

## Pilares de diseño
1. **Sensación de golpe**: hit-stop, screen shake, destello blanco al impactar, números de daño, chispas y knockback.
2. **Decisiones significativas**: cada subida de nivel ofrece 3 perks (4 con metaprogreso) con rareza y sinergias.
3. **Progreso que persiste**: la moneda *mon* (文) se gasta en un santuario con mejoras permanentes y desbloqueos.
4. **Legibilidad en el caos**: los ataques de jefe se telegrafían, las balas enemigas contrastan con el suelo y hay indicadores fuera de pantalla.

## Bucle de juego
- Vista cenital, cámara que sigue al jugador en una arena de 3000×3000 px con límites de neón.
- **Movimiento** WASD/flechas, **dash** con Espacio/Shift/clic derecho (i-frames y cooldown). **Ataque automático** apuntando al enemigo más cercano (opción de apuntar con ratón).
- **3 actos** de 2:30 cada uno; al terminar el tiempo aparece el jefe. Al vencerlo sueltan un cofre (perk raro garantizado) y se abre un torii-portal hacia el siguiente acto. Vencer al tercer jefe es la victoria.
- Cada 40 s, evento **百鬼夜行 Night Parade**: un anillo de enemigos rodea al jugador.
- Los enemigos sueltan orbes de experiencia (*tama*), monedas *mon*, onigiri (curación) y a veces una campanilla que atrae todos los orbes.
- Enemigos élite (dorados, 4× vida, más botín) y escalado por tiempo y acto.

## Personajes (desbloqueables)
| Personaje | Arma | Rasgo |
|---|---|---|
| **Rōnin 浪人** | Katana en arco | Corta a corto alcance y **desvía balas** enemigas |
| **Kunoichi くノ一** (300 文) | Shuriken perforantes | Rápida y frágil, dash más corto |
| **Onmyōji 陰陽師** (550 文) | Ofuda teledirigidos | Empieza con un orbe de Foxfire |

## Enemigos (yokai)
Chōchin-obake (farol flotante), Kasa-obake (paraguas que salta), Kappa (embiste tras una carga visible), Yūrei (fantasma que zigzaguea y parpadea), Tengu (dispara plumas a distancia), Oni (tanque resistente al empuje).

## Jefes (con fase de furia al 50 %)
1. **Gashadokuro 餓者髑髏**: anillos de huesos, golpes de mano telegrafiados con círculo, invocación de faroles.
2. **Kyūbi no Kitsune 九尾狐**: espirales de fuego fatuo, teletransporte con abanico de balas, embestida que deja llamas.
3. **Shuten-dōji 酒呑童子**: cargas en línea, ondas de choque expansivas (se esquivan con dash), rociada de sake, invoca onis.

## Perks al subir de nivel (≈30)
Rarezas **並 común / 稀 raro / 伝説 legendario**, con peso afectado por la *suerte*. Tipos:
- **Estadísticas**: daño, velocidad de ataque, área, crítico, vida, velocidad, imán, armadura, regeneración, XP, mon.
- **Técnicas activas**: Raijin (rayos periódicos), Foxfire (orbes orbitales que queman), Senbonzakura (aura de pétalos), Tengu Gust (onda que empuja), Gale Dash (el dash corta), Kekkai (escudo que bloquea un golpe y se recarga).
- **Procs**: Yuki-onna (congelar), Hellfire (quemadura), Blood Oath (robo de vida).
- **Legendarios**: Kaishaku (ejecutar por debajo del 15 %), Hō-ō (revivir), Kishin (daño alto a cambio de vida), Hyakki Echo (cada 4.º ataque se repite).
- Perks exclusivos por personaje (Iaijutsu para el Rōnin, perforación para armas de proyectil).
- Opción de **re-tirar** las cartas (cargas de metaprogreso) y cartas de relleno cuando todo está al máximo.

## Metaprogreso: el santuario (神社)
Mejoras permanentes compradas con mon: vida, daño, velocidad, armadura, imán, XP, mon extra, re-tiradas, *Omamori* (revivir), *Fourth Path* (4 cartas por nivel), suerte. Desbloqueo de personajes. Al ganar se desbloquea la **dificultad Kurayami 闇 (0 a 5)**: más vida y velocidad de enemigos a cambio de más mon.
Se guarda en `localStorage` junto con estadísticas (partidas, victorias, muertes, mejor acto) y ajustes.

## Dirección visual
- Paleta: tinta casi negra con tinte índigo, rosa neón `#ff2e88`, cian `#29e7ff`, oro `#ffd23f`, bermellón. Cada acto tiene su color de acento.
- **Acto I Kabukichō**: callejones con lluvia, charcos, letreros verticales (ラーメン, 居酒屋, カラオケ), máquinas expendedoras, guirnaldas de faroles.
- **Acto II Fushimi Inari**: torii bermellón, tōrō de piedra, estatuas de zorro, fuegos fatuos, pétalos.
- **Acto III Ōeyama**: fortaleza oni, grietas de lava, braseros, pilares con shimenawa, ascuas que suben.
- Sprites procedurales pre-renderizados en canvas offscreen con glow; halos aditivos (`lighter`) cacheados para rendimiento. Viñeta, clima por acto y estela de bufanda.
- Menú principal: ciudad de neón con el monte Fuji, pagoda, sol rayado synthwave, suelo en perspectiva y lluvia. Logo vertical ネオン浪人.
- Tipografía: Dela Gothic One (display), Zen Kaku Gothic New (texto), DotGothic16 (números del HUD).

## Audio (Web Audio, 100 % sintetizado)
Música generativa en escala *in* (D, E♭, G, A, B♭): koto con reverb, bajo, taiko, hi-hats; modos menú / combate / jefe con distinto tempo. SFX de corte, impacto, crítico, recogida con tono ascendente, subida de nivel, rayo, rugido de jefe.

## UI
Título, selección de personaje, santuario, subida de nivel con cartas animadas (teclas 1-4, R para re-tirar), pausa con resumen de build, pantalla final con desglose de mon, ajustes (volumen, música, shake, números de daño, apuntado con ratón, borrar progreso con confirmación en dos pasos). HUD con vida, XP, nivel, temporizador, muertes, mon, perks y cooldown del dash, barra de jefe.
Controles táctiles: joystick virtual y botón de dash. Pausa automática al perder el foco.

## Requisitos técnicos
- Un solo archivo, sin librerías. Bucle con `requestAnimationFrame` y delta limitado.
- Rejilla espacial para colisiones y separación de enemigos; límite de partículas y balas.
- Escalado de vista según tamaño de pantalla; soporte DPR.
- Todo el acceso a `localStorage` dentro de try/catch.
- `prefers-reduced-motion` reduce animaciones de UI.
