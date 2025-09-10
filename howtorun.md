Para reiniciar FluffyChat en tu navegador después de reiniciar tu PC, necesitarás ejecutar estos comandos:

  Comandos para reiniciar FluffyChat:

  # 1. Navegar al directorio del proyecto
  cd /home/andres/Documents/nexxo/fluffychat

  # 2. Iniciar el servidor web (opción más rápida)
  cd build/web && python3 -m http.server 8080

  Luego abre tu navegador en: http://localhost:8080

  Alternativa - Modo desarrollo con hot reload:

  # 1. Navegar al directorio del proyecto
  cd /home/andres/Documents/nexxo/fluffychat

  # 2. Ejecutar Flutter en modo desarrollo
  ~/development/flutter/bin/flutter run -d chrome --web-port 8080

  Si necesitas recompilar (solo si hiciste cambios):

  cd /home/andres/Documents/nexxo/fluffychat
  ~/development/flutter/bin/flutter build web --release
  cd build/web && python3 -m http.server 8080

  Recomendación:

  Para mayor comodidad, puedes crear un alias en tu .bashrc:

  echo 'alias fluffychat="cd /home/andres/Documents/nexxo/fluffychat/build/web && python3 -m http.server 8080"' >> ~/.bashrc
  source ~/.bashrc

  Después solo ejecuta: fluffychat y abre http://localhost:8080
