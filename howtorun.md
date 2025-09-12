# FluffyChat - Guía de Desarrollo y Ejecución

## 🚀 Ejecución Rápida

### Modo Desarrollo (Recomendado para desarrollo)
Con hot reload automático - los cambios se aplican al instante:

```bash
# Navegar al directorio del proyecto
cd /home/andres/Documents/nexxo/fluffychat

# Ejecutar Flutter en modo desarrollo con hot reload
~/development/flutter/bin/flutter run -d chrome --web-port 8080
```

**Ventajas del modo desarrollo:**
- ✅ Hot reload automático (cambios instantáneos)
- ✅ DevTools de Flutter disponibles
- ✅ Debugging completo
- ✅ No necesitas recompilar para ver cambios

**Comandos durante la ejecución:**
- `r` - Hot reload manual
- `R` - Hot restart (reiniciar app completa)  
- `q` - Salir
- `h` - Ver todos los comandos disponibles

### Modo Producción (Solo para servir archivos compilados)
Para servir la versión compilada estática:

```bash
# Navegar al directorio del proyecto
cd /home/andres/Documents/nexxo/fluffychat

# Servir archivos estáticos compilados
cd build/web && python3 -m http.server 8080
```

**Cuándo usar este modo:**
- ✅ Para probar la versión final de producción
- ✅ Cuando solo necesitas mostrar la app sin desarrollar
- ❌ NO para desarrollo activo (sin hot reload)

---

## 🔧 Desarrollo y Compilación

### Preparar el entorno (solo la primera vez)
```bash
# Instalar dependencias
~/development/flutter/bin/flutter pub get

# Preparar assets para web (necesario para crypto)
./scripts/prepare-web.sh
```

### Compilar para producción
```bash
# Compilar versión optimizada para producción
~/development/flutter/bin/flutter build web --release

# Luego servir los archivos compilados
cd build/web && python3 -m http.server 8080
```

### Comandos útiles durante desarrollo
```bash
# Análisis de código
~/development/flutter/bin/flutter analyze

# Formatear código
dart format lib/ test/

# Ejecutar tests
~/development/flutter/bin/flutter test
```

---

## 🛠️ Alias útiles

Para mayor comodidad, agregar estos alias a tu `~/.bashrc`:

```bash
# Modo desarrollo con hot reload
alias fluffydev="cd /home/andres/Documents/nexxo/fluffychat && ~/development/flutter/bin/flutter run -d chrome --web-port 8080"

# Servir versión compilada
alias fluffyprod="cd /home/andres/Documents/nexxo/fluffychat/build/web && python3 -m http.server 8080"

# Compilar para producción
alias fluffybuild="cd /home/andres/Documents/nexxo/fluffychat && ~/development/flutter/bin/flutter build web --release"
```

Para aplicar los alias:
```bash
source ~/.bashrc
```

Después solo ejecuta:
- `fluffydev` - Para desarrollo con hot reload
- `fluffyprod` - Para servir versión de producción  
- `fluffybuild` - Para compilar nueva versión

---

## 📖 URLs de Acceso

- **Aplicación**: http://localhost:8080
- **Flutter DevTools** (solo en modo dev): Se muestra en la consola cuando ejecutas el modo desarrollo

---

## 🔄 Workflow Recomendado

1. **Para desarrollo diario**: Usar `fluffydev` (modo desarrollo)
2. **Para ver cambios**: Simplemente guarda los archivos - hot reload automático
3. **Para producción final**: Usar `fluffybuild` y luego `fluffyprod`

---

## 🆘 Solución de Problemas

### Puerto 8080 ocupado
```bash
# Ver qué proceso usa el puerto
netstat -tlnp | grep :8080

# Terminar proceso en puerto 8080
fuser -k 8080/tcp
```

### Problemas de compilación
```bash
# Limpiar cache de Flutter
~/development/flutter/bin/flutter clean

# Reinstalar dependencias
~/development/flutter/bin/flutter pub get

# Preparar web assets nuevamente
./scripts/prepare-web.sh
```