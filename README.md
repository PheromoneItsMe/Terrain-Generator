# 3D Terrain & City Generator for Blender

[![Blender](https://img.shields.io/badge/Blender-4.0%20%7C%204.1%20%7C%204.2%20%7C%205.0%2B-orange.svg?logo=blender)](https://www.blender.org/)
[![Version](https://img.shields.io/badge/Version-1.4.0-blue.svg)]()
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Author](https://img.shields.io/badge/Author-Pheromone-lightgrey.svg)]()

A high-performance Blender add-on for generating physically accurate 3D terrains, road networks, waterways, and complete urban & rural building environments for any coordinate or place on Earth.

---

## English Documentation

### Overview

**3D Terrain & City Generator** automates the entire geospatial reconstruction pipeline directly inside Blender. By unifying radar satellite elevation tiles, a global dataset of 1.4+ billion building footprints, and OpenStreetMap vector infrastructure, it creates ready-to-render 3D environments in seconds.

### Key Features

* **100% Building Completeness (Global Satellite Footprint Dataset)**:
  * Solves the major limitation of standard volunteer-mapped OpenStreetMap data, where rural settlements, villages, and private residential quarters often miss 50–70% of structures.
  * Connects directly to the global satellite building dataset (**1.4+ billion footprints worldwide**).
  * Automatically calculates spatial indices (**Bing Quadkeys Level 9**) to fetch and cache compressed footprint tiles for any country or territory.
* **Physically Accurate NASA SRTM Elevation**:
  * Stitches high-detail Terrarium / NASA SRTM radar elevation tiles seamlessly across bounding coordinates.
  * Resamples heights using bilinear interpolation with adaptive Gaussian smoothing to eliminate radar speckle artifacts while preserving natural mountain ridges.
* **Vector Road & Water Networks**:
  * Extracts highways, secondary thoroughfares, and residential alleys from OpenStreetMap.
  * Directly snaps road meshes and riverbeds onto the terrain surface using mathematical raycasting, preventing floating geometry.
* **Architectural Shading & CAD Cavity Outlines**:
  * Automatic multi-material setup: ambient-occluded off-white walls, per-building randomized terracotta and slate roofs, paved road ribbons, and reflective water.
  * Native hardware-accelerated Cavity and Ridge outlines for architectural maquette presentation without modifier overhead.
* **Intelligent Input Geocoding**:
  * **Google Maps URLs**: Paste full links directly (e.g. `https://www.google.com/maps/@41.20109,44.22910,2500m`) to auto-detect center coordinates and camera altitude.
  * **Direct Coordinates**: Enter `latitude, longitude` (e.g. `40.1792, 44.4991`).
  * **Place Names**: Fast Nominatim geocoding with balanced urban bounding boxes.
* **Rock-Solid Stability**:
  * Bakes static geometry directly into GPU vertex buffers.
  * Completely avoids heavyweight live Boolean or shrinkwrap modifier loops, guaranteeing zero crashes and instantaneous viewport playback.

---

### Installation

1. Download [`terrain_generator_addon.py`](terrain_generator_addon.py) from this repository.
2. In Blender, navigate to:
   **Edit** > **Preferences** > **Add-ons** > **Install...** (or arrow menu in Blender 4.2+ > *Install from Disk...*).
3. Select `terrain_generator_addon.py` and enable the checkbox **3D Terrain & City Generator**.
4. The add-on panel will appear in the 3D Viewport sidebar (`N` key) under the **Terrain Generator** tab.

---

### How to Use

1. Press `N` in the 3D Viewport and open the **Terrain Generator** panel.
2. Under **1. Location Search**, enter a place name, raw coordinates, or paste a Google Maps link.
3. Select the desired building source:
   * **Satellite Footprints (100% Buildings)**: Recommended. Full satellite-detected roof coverage everywhere.
   * **Hybrid (Satellite + OSM)**: Satellite geometry merged with OpenStreetMap tags.
   * **OpenStreetMap (Classic)**: Standard OSM volunteer vectors.
4. Customize terrain grid resolution (`120x120`, `180x180`, `240x240`), height exaggeration, and roof style.
5. Click **🚀 GENERATE 3D MAP**.
6. The scene, lighting, and camera will be generated in 4–8 seconds.

---

### Parameter Reference

| Setting | Type | Description |
| :--- | :--- | :--- |
| **Location Query** | String | City name, coordinates (`lat, lon`), or Google Maps link. |
| **Auto-Span** | Boolean | Automatically derives capture area from camera altitude or city boundaries. |
| **Area Size (km)** | Float | Custom bounding box width in kilometers (1.5 to 30.0 km). |
| **Grid Resolution** | Enum | Elevation mesh density (`120x120`, `180x180`, `240x240`). |
| **Height Exaggeration Z** | Float | Vertical multiplier for dramatic mountain and slope readability (default: `2.2`). |
| **Building Source** | Enum | Dataset source: `SATELLITE` (100% complete), `HYBRID`, or `OSM`. |
| **Use Real OSM Heights** | Boolean | Parses architectural floors and meter heights where available. |
| **Default Wall Height** | Float | Baseline wall height for un-tagged structures. |
| **Roof Style** | Enum | Roof color palette: `TERRACOTTA`, `SLATE`, or `WHITE`. |
| **CAD Outlines** | Boolean | Enables crisp architectural edge cavity contours in viewport. |

---

## Русская документация

### Описание

**3D Terrain & City Generator** — это профессиональный инструмент для Blender, автоматизирующий создание точных 3D-ландшафтов, дорожных сетей, водоёмов и полноценной городской и сельской застройки для любой точки мира.

### Ключевые возможности

* **100% застройка по глобальным спутниковым данным (1.4+ млрд зданий)**:
  * Устраняет главную проблему стандартного OpenStreetMap: в деревнях, сёлах и частном секторе волонтеры не успевают вручную оцифровать 50–70% домов и строений.
  * Интегрирован глобальный массив спутникового распознавания крыш (**1.4 миллиарда строений по всему миру**).
  * Автоматический расчет пространственных квадрантов (**Bing Quadkeys Level 9**) с мгновенной локальной загрузкой и кэшированием тайлов.
* **Физически достоверный рельеф NASA SRTM**:
  * Бесшовная сшивка нескольких радарных тайлов Terrarium / NASA SRTM на заданной территории.
  * Билинейная интерполяция высот с мягкой фильтрацией шумов радарного сканирования при полном сохранении горных хребтов и ущелий.
* **Векторная инфраструктура и водоёмы**:
  * Построение автодорог (трассы, городские проспекты, проселочные улицы) и русел рек.
  * Математическая привязка (raycast) дорожного полотна и фундаментов домов точно к поверхности рельефа — исключает зависание объектов в воздухе.
* **Архитектурные шейдеры и чертежные контуры CAD**:
  * Готовые процедурные материалы: стены с мягким Ambient Occlusion, крыши с индивидуальной вариацией черепичных и сланцевых оттенков, асфальт и вода.
  * Аппаратно-ускоренные контуры рёбер (Cavity / Ridge) в стиле архитектурного макета без нагрузки на модификаторы.
* **Универсальный поиск**:
  * **Ссылки Google Maps**: Вставка ссылки прямо из браузера (`@lat,lon,alt`) с автоопределением центра и высоты обзора.
  * **Координаты**: Прямой ввод широты и долготы через запятую (например, `41.201, 44.229`).
  * **Названия**: Поиск городов, сёл и природных объектов через Nominatim.
* **Абсолютная стабильность без сбоев**:
  * Прямая запись статической геометрии в буферы меша. Отсутствие тяжелых модификаторов гарантирует быструю работу во Viewport без риска вылетов Blender.

---

### Установка

1. Скачайте файл [`terrain_generator_addon.py`](terrain_generator_addon.py).
2. В Blender откройте меню:
   **Edit** (Правка) > **Preferences** (Настройки) > **Add-ons** (Аддоны) > **Install...** (Установить из файла).
3. Выберите файл `terrain_generator_addon.py` и включите галочку у аддона **3D Terrain & City Generator**.
4. Панель аддона появится на боковой панели 3D Viewport (клавиша `N`) во вкладке **Terrain Generator**.

---

### Пошаговое руководство

1. Нажмите клавишу `N` в окне 3D Viewport и перейдите во вкладку **Terrain Generator**.
2. В поле **1. Поиск местности** введите название города/села, координаты или вставьте ссылку на Google Карты.
3. Выберите источник зданий:
   * **🛰️ Спутниковый датасет (100% домов)**: Рекомендуется. Дает полную застройку всех домов и частного сектора.
   * **⚡ Гибрид (Спутник + Данные OSM)**: Спутниковые контуры крыш + названия и высоты OpenStreetMap.
   * **🗺️ OpenStreetMap (Классика)**: Только ручные данные OpenStreetMap.
4. Настройте плотность сетки рельефа, множитель высоты Z и стиль крыш.
5. Нажмите кнопку **🚀 СГЕНЕРИРОВАТЬ 3D-КАРТУ**.
6. Через 4–8 секунд готовая модель появится в сцене в режиме Material Preview.

---

## Архитектура и стек данных

* **Среда выполнения**: Blender 4.0+, 4.1, 4.2, 5.0+ (Python 3.10+)
* **Данные рельефа**: NASA SRTM / AWS Terrarium Elevation Tiles
* **Данные зданий**: Global Satellite Footprints Dataset (Bing Maps / Maxar / Airbus / IGN)
* **Данные дорог и гидрографии**: OpenStreetMap Vector API / Overpass API
* **Геокодирование**: Nominatim OpenStreetMap

---

## License & Author

* **Author**: [Pheromone](https://github.com/PheromoneItsMe)
* **License**: [MIT License](LICENSE)
