# Single Kill Notification — Lyra

Реализация системы уведомлений об одиночном убийстве (Single Kill) с использованием **Gameplay Message Subsystem** и **UI Extension System** в Lyra.

<p align="center">
  <img src="Images/test1.gif" width="600" alt="Single Kill Notification">
</p>

## 1. UI Extension Point

В виджет `W_ShooterHUDLayout` добавлен `ExtensionPoint` со следующими параметрами:

- **Slot ID:** `HUD.Slot.SingleKill`

Данный слот используется для отображения уведомлений об убийстве.

## 2. Виджеты уведомлений

Созданы два виджета:

- `W_SingleKillNotification` — отображает уведомление об убийстве и проигрывает анимацию.
- `W_SingleKillHostWidget` — контейнер для создания и управления уведомлениями.

### Регистрация Host Widget

`W_SingleKillHostWidget` добавлен в `LAS_ShooterGame_StandardHUD` со следующими параметрами:

- **Slot ID:** `HUD.Slot.SingleKill`
- **Widget:** `W_SingleKillHostWidget`

### Логика W_SingleKillHostWidget

В виджете реализована подписка на Gameplay Message:

`Lyra.AddNotification.SingleKill`

При получении сообщения:

1. Создаётся экземпляр `W_SingleKillNotification`.
2. Созданный виджет добавляется в `W_SingleKillHostWidget` как дочерний элемент.
3. Запускается анимация уведомления.
4. После завершения анимации уведомление удаляется из контейнера.

## 3. Обработка событий убийства

Создан Blueprint `B_SingleKillRelay`.

### Логика B_SingleKillRelay

Реализована подписка на Gameplay Message:

`Lyra.Elimination.Message`

При получении сообщения об убийстве на клиенте выполняется **Broadcast** следующего Gameplay Message:

`Lyra.AddNotification.SingleKill`

### Регистрация компонента

`B_SingleKillRelay` добавлен в `EAS_BasicShooterAcolades`.

**Тип компонента:** `Client + Server`
