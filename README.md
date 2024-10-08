# Домашнее задание к занятию 17 «Инцидент-менеджмент»

## Основная часть

Составьте постмортем на основе реального сбоя системы GitHub в 2018 году.

Информация о сбое: 

* [в виде краткой выжимки на русском языке](https://habr.com/ru/post/427301/);
* [развёрнуто на английском языке](https://github.blog/2018-10-30-oct21-post-incident-analysis/).

## Задание 

Составьте постмортем, на основе реального сбоя системы Github в 2018 году.

Информация о сбое доступна [в виде краткой выжимки на русском языке](https://habr.com/ru/post/427301/) , а
также [развёрнуто на английском языке](https://github.blog/2018-10-30-oct21-post-incident-analysis/).

## Ответ

Название | Описание
--- | ---
Краткое описание инцидента | 21.10.2018 в 22:52 по UTC пострадали несколько сервисов на GitHub.com, несколько сетевых разделов c последующим сбоем базы данных, что привело к несогласованной информации, представленной на веб-сайте
Предшествующие события | 21 октября в 22:52 UTC в результате регламентных работ по замене вышедшего из строя оптического оборудования 100G
Причина инцидента | Потеря связи между сетевым концентратором на восточном побережье США и основным центром обработки данных на восточном побережье США
Воздействие | В большинстве случаев GitHub не мог обслуживать события веб-перехватчиков или создавать и публиковать GitHub Pages
Обнаружение | 21 октября 22:54 UTC системы мониторинга начали генерировать предупреждения. В 23:02 UTC инженеры группы быстрого реагирования определили, что топологии многочисленных кластеров баз данных находятся в непредвиденном состоянии
Реакция | Связь между точками была восстановлена за 43 секунды, но этот кратковременный сбой вызвал цепочку событий, которые привели к ухудшению качества обслуживания на 24 часа 11 минут
Восстановление | Восстановлены из резервных копий данные MySQL, синхронизированы реплики на обоих сайтах, произведён возврат к стабильной топологии обслуживания, возобновлена обработка заданий в очереди
Таймлайн | `21 октября 22:52 UTC` Аварийное переключение кластеров для направления операций записи в ЦОД на западном побережье США <br /> `21 октября 22:54 UTC` Системы мониторинга начали генерировать предупреждения, указывающие на многочисленные сбои в системах <br /> `21 октября 23:07 UTC` Команда решила вручную заблокировать внутренний инструмент развертывания, чтобы предотвратить внесение каких-либо дополнительных изменений <br /> `21 октября 23:13 UTC` Были вызваны дополнительные инженеры из группы разработки баз данных GitHub <br /> `21 октября 23:19 UTC`  Приостановка доставки веб-перехватчика и сборки страниц GitHub <br /> `22 октября 00:05 UTC` Разработка плана по устранению несоответствий данных и внедрения процедур аварийного переключения для MySQL <br /> `22 октября 00:41 UTC` Инициирован процесс резервного копирования для всех затронутых кластеров MySQL <br /> `22 октября 06:51 UTC` Несколько кластеров завершили восстановление из резервных копий в центре обработки данных на восточном побережье США и начали репликацию новых данных с западного побережья <br /> `22 октября 07:46 UTC` GitHub опубликовал сообщение в блоге, чтобы предоставить больше информации <br /> `22 октября 11:12 UTC` Все первичные базы данных снова установлены на восточном побережье США <br /> `22 октября 13:15 UTC` Стали приближаться к пиковой нагрузке трафика на GitHub.com <br /> `22 октября 16:24 UTC` Выполнено аварийное переключение на исходную топологию, решив проблемы с задержкой/доступностью <br /> `22 октября 16:45 UTC` Балансировка возросшей нагрузки, созданной отставанием  <br /> `22 октября 23:03 UTC` Все задачи ожидающие сборки вебхуков и страниц были обработаны, и была подтверждена целостность и правильная работа всех систем
Последующие действия | Определен ряд технических инициатив: <br /> 1. Настройка конфигурацию Orchestrator, чтобы предотвратить движение основных баз данных через региональные границы <br /> 2. Ускорить переход на новый механизм отчетов о состоянии, который предоставит более богатую площадку для обсуждения активных инцидентов, более четким и понятным языком <br /> 3. Поддержка обслуживания трафика GitHub из нескольких центров обработки данных по схеме «активный/активный/активный» <br /> 4. Занять более активную позицию в проверке предположений
---

