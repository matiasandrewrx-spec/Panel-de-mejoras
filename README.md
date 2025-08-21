<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Panel de Mejoras - Servicio Técnico EMOCH</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals (Slate, Zinc, Amber) -->
    <!-- Application Structure Plan: Se ha diseñado una aplicación de panel de control (dashboard) con una barra de navegación lateral fija. Esta estructura permite al usuario cambiar fácilmente entre las distintas áreas del taller (Taller, Sala de Lavado, etc.) sin perder el contexto. Cada área presenta sus puntos de mejora en un formato de tarjetas visuales, lo que facilita la asimilación de la información. Se incluye una sección de "Resumen" con un gráfico para ofrecer una vista general del proyecto. Esta arquitectura fue elegida por su claridad, interactividad y familiaridad para el usuario, transformando una lista de tareas en un plan de proyecto explorable. -->
    <!-- Visualization & Content Choices: 
        - Resumen: Donut Chart (Chart.js) para mostrar la distribución de tareas por área. Objetivo: Informar de un vistazo sobre el alcance del proyecto en cada sección. Interacción: Tooltip al pasar el cursor. Justificación: Es una visualización clara y concisa para datos categóricos.
        - Puntos de Mejora: Tarjetas (HTML/Tailwind) con iconos (Unicode). Objetivo: Organizar y presentar cada tarea de forma individual y clara. Interacción: Botón de estado para simular el seguimiento del proyecto. Justificación: Las tarjetas separan visualmente cada punto, mejorando la legibilidad. Los iconos (ej: ⚠️ para seguridad) comunican la naturaleza de la tarea rápidamente.
        - Navegación: Lista de enlaces con estado activo (JS). Objetivo: Permitir una navegación fluida e intuitiva entre las secciones. Interacción: Clic para cambiar de vista. Justificación: Es un patrón de navegación estándar y efectivo para SPAs.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc; /* slate-50 */
        }
        .nav-link {
            transition: all 0.2s ease-in-out;
        }
        .nav-link.active {
            background-color: #f59e0b; /* amber-500 */
            color: #ffffff;
            font-weight: 600;
        }
        .nav-link:not(.active):hover {
            background-color: #e2e8f0; /* slate-200 */
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
            height: 320px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .status-btn {
            transition: background-color 0.2s ease-in-out;
        }
    </style>
</head>
<body class="text-slate-800">
    <div class="flex h-screen">
        <aside class="w-64 bg-white border-r border-slate-200 flex-shrink-0">
            <div class="p-6">
                <h1 class="text-2xl font-bold text-slate-900">Servicio Técnico</h1>
                <p class="text-sm text-slate-500">Plan de Mejoras EMOCH</p>
            </div>
            <nav class="mt-4">
                <ul>
                    <li><a href="#" class="nav-link active block py-3 px-6" data-target="resumen">📊 Resumen General</a></li>
                    <li><a href="#" class="nav-link block py-3 px-6" data-target="taller">🔧 Taller Principal</a></li>
                    <li><a href="#" class="nav-link block py-3 px-6" data-target="lavado">💧 Sala de Lavado</a></li>
                    <li><a href="#" class="nav-link block py-3 px-6" data-target="pruebas">🔬 Sala de Pruebas</a></li>
                    <li><a href="#" class="nav-link block py-3 px-6" data-target="bodega">📦 Bodega</a></li>
                </ul>
            </nav>
        </aside>

        <main class="flex-1 p-6 md:p-10 overflow-y-auto">
            <div id="resumen" class="content-section">
                <h2 class="text-3xl font-bold mb-2">Resumen del Proyecto</h2>
                <p class="text-slate-600 mb-8">Vista general de las mejoras propuestas para el Servicio Técnico. Navega por las secciones en el menú lateral para ver el detalle de cada área.</p>
                <div class="bg-white p-6 rounded-lg shadow-sm">
                    <h3 class="text-xl font-semibold mb-4">Puntos de Mejora por Área</h3>
                    <div class="chart-container">
                        <canvas id="tasksChart"></canvas>
                    </div>
                </div>
            </div>

            <div id="taller" class="content-section hidden">
                <h2 class="text-3xl font-bold mb-2">🔧 Taller Principal</h2>
                <p class="text-slate-600 mb-8">Mejoras enfocadas en la infraestructura base, el orden y la apariencia del área de trabajo principal para aumentar la eficiencia y seguridad.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🏢 Implementación de Porcelanato</h3>
                        <p class="text-sm text-slate-600 mb-4">Instalar porcelanato en el suelo para mejorar la limpieza, durabilidad y apariencia general del taller.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">💨 Mejora de Ventilación</h3>
                        <p class="text-sm text-slate-600 mb-4">Instalar extractores y ventiladores de admisión para renovar el aire y mejorar las condiciones ambientales.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🧹 Orden y Limpieza</h3>
                        <p class="text-sm text-slate-600 mb-4">Despejar los mesones de trabajo de objetos y herramientas innecesarias para optimizar el espacio.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">✨ Cambio de Paneles Sombra</h3>
                        <p class="text-sm text-slate-600 mb-4">Reemplazar los paneles de herramientas debido a su mal estado y suciedad impregnada.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🎨 Pintado de Paredes</h3>
                        <p class="text-sm text-slate-600 mb-4">Pintar las paredes con pintura resistente a la humedad para combatir la suciedad y el deterioro.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                </div>
            </div>

            <div id="lavado" class="content-section hidden">
                <h2 class="text-3xl font-bold mb-2">💧 Sala de Lavado</h2>
                <p class="text-slate-600 mb-8">Acciones para mejorar la higiene, seguridad y funcionalidad del área destinada a la limpieza de maquinaria.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🧹 Limpieza General</h3>
                        <p class="text-sm text-slate-600 mb-4">Realizar limpieza profunda de paredes y techo, y mantenerla diariamente para conservar la armonía.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">💧 Mejora de Drenaje</h3>
                        <p class="text-sm text-slate-600 mb-4">Corregir la canaleta central para evitar el estancamiento de agua y la generación de malos olores.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🗑️ Despeje de Residuos</h3>
                        <p class="text-sm text-slate-600 mb-4">Retirar tambores de aceite y tarros vacíos para liberar espacio y mejorar el orden.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🏢 Nuevos Mesones de Lavado</h3>
                        <p class="text-sm text-slate-600 mb-4">Implementar mesones de lavado en mejor estado, más prácticos y resistentes para la tarea.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                </div>
            </div>

            <div id="pruebas" class="content-section hidden">
                <h2 class="text-3xl font-bold mb-2">🔬 Sala de Pruebas</h2>
                <p class="text-slate-600 mb-8">Intervenciones críticas para garantizar la seguridad, el cumplimiento normativo y la funcionalidad de la sala de pruebas de equipos.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">⚠️ Reparación de Mesón</h3>
                        <p class="text-sm text-slate-600 mb-4">Cambiar revestimiento metálico roto del mesón que pone en peligro la integridad física del técnico.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🔇 Cambio de Esponjas Acústicas</h3>
                        <p class="text-sm text-slate-600 mb-4">Reemplazar las esponjas acústicas debido a su mal estado para mejorar el aislamiento del sonido.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">📜 Chequeo Normativo Extractores</h3>
                        <p class="text-sm text-slate-600 mb-4">Verificar que los extractores cumplan con la normativa de ventilación en espacios cerrados (N°594 Art. 32).</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">💨 Ventilación Adicional</h3>
                        <p class="text-sm text-slate-600 mb-4">Instalar ventiladores de admisión para renovar los gases que quedan en la sala.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">⚡ Cambio Caja de Enchufe</h3>
                        <p class="text-sm text-slate-600 mb-4">Reemplazar la caja de enchufes del sector por seguridad eléctrica.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">⚠️ Reubicar Equipos Peligrosos</h3>
                        <p class="text-sm text-slate-600 mb-4">Cambiar de posición el esmeril y la soldadora, ya que su uso en la sala es peligroso.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">💡 Mejorar Iluminación</h3>
                        <p class="text-sm text-slate-600 mb-4">Aumentar y mejorar la iluminación de la sala para facilitar el trabajo de precisión.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                </div>
            </div>

            <div id="bodega" class="content-section hidden">
                <h2 class="text-3xl font-bold mb-2">📦 Bodega</h2>
                <p class="text-slate-600 mb-8">Propuestas para organizar el almacenamiento, mejorar la clasificación y optimizar la gestión de equipos y chatarra.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🧹 Orden de Chatarra</h3>
                        <p class="text-sm text-slate-600 mb-4">Realizar orden y limpieza en el sector izquierdo donde se almacena la chatarra.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-sm">
                        <h3 class="text-lg font-semibold mb-2">🏷️ Sistema de Clasificación</h3>
                        <p class="text-sm text-slate-600 mb-4">Añadir letreros para equipos (reparados, presupuestados, en espera) para mejorar la organización.</p>
                        <button class="status-btn text-xs font-medium py-1 px-3 rounded-full" data-status="pendiente">Pendiente</button>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const navLinks = document.querySelectorAll('.nav-link');
            const contentSections = document.querySelectorAll('.content-section');
            const statusButtons = document.querySelectorAll('.status-btn');

            const statusConfig = {
                'pendiente': { text: 'Pendiente', color: 'bg-red-200', textColor: 'text-red-800' },
                'en-progreso': { text: 'En Progreso', color: 'bg-yellow-200', textColor: 'text-yellow-800' },
                'completado': { text: 'Completado', color: 'bg-green-200', textColor: 'text-green-800' }
            };

            function updateButtonState(button, status) {
                const config = statusConfig[status];
                button.textContent = config.text;
                button.dataset.status = status;
                
                Object.values(statusConfig).forEach(c => {
                    button.classList.remove(c.color, c.textColor);
                });
                button.classList.add(config.color, config.textColor);
            }

            navLinks.forEach(link => {
                link.addEventListener('click', (e) => {
                    e.preventDefault();
                    
                    navLinks.forEach(l => l.classList.remove('active'));
                    link.classList.add('active');
                    
                    const targetId = link.dataset.target;
                    
                    contentSections.forEach(section => {
                        if (section.id === targetId) {
                            section.classList.remove('hidden');
                        } else {
                            section.classList.add('hidden');
                        }
                    });
                });
            });

            statusButtons.forEach(button => {
                updateButtonState(button, 'pendiente');
                button.addEventListener('click', () => {
                    let currentStatus = button.dataset.status;
                    let nextStatus;
                    if (currentStatus === 'pendiente') nextStatus = 'en-progreso';
                    else if (currentStatus === 'en-progreso') nextStatus = 'completado';
                    else nextStatus = 'pendiente';
                    updateButtonState(button, nextStatus);
                });
            });

            const taskData = {
                labels: ['Taller Principal', 'Sala de Lavado', 'Sala de Pruebas', 'Bodega'],
                datasets: [{
                    label: 'Puntos de Mejora',
                    data: [5, 4, 7, 2],
                    backgroundColor: [
                        'rgba(59, 130, 246, 0.8)',  // blue-500
                        'rgba(34, 197, 94, 0.8)',  // green-500
                        'rgba(239, 68, 68, 0.8)',   // red-500
                        'rgba(107, 114, 128, 0.8)' // gray-500
                    ],
                    borderColor: '#ffffff',
                    borderWidth: 3,
                    hoverOffset: 8
                }]
            };

            const config = {
                type: 'doughnut',
                data: taskData,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                font: {
                                    size: 14,
                                    family: 'Inter'
                                }
                            }
                        },
                        tooltip: {
                            padding: 12,
                            titleFont: {
                                size: 16,
                                family: 'Inter',
                                weight: 'bold'
                            },
                            bodyFont: {
                                size: 14,
                                family: 'Inter'
                            }
                        }
                    },
                    cutout: '60%'
                }
            };
            
            const tasksChartCtx = document.getElementById('tasksChart').getContext('2d');
            new Chart(tasksChartCtx, config);
        });
    </script>
</body>
</html>
