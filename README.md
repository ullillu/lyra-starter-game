В рамках тестового задания было выполнено:


1. В W\_ShooterHUDLayout добавлен ExtensionPoint со SlotID = HUD.Slot.SingleKill



2\. Созданы 2 виджета - W\_SingleKillNotification, W\_SingleKillHostWidget



W\_SingleKillHostWidget добавлен в LAS\_ShooterGame\_StandardHUD, SlotID = HUD.Slot.SingleKill



В W\_SingleKillHostWidget  реализована подписка на сообщение Lyra.AddNotification.SingleKill. На эвент получения сообщения создается W\_SingleKillNotification, который добавляется в хост-виджет как чайлд. На окончание анимации, виджет удаляется.



3\. Создан B\_SingleKillRelay. В нем реализована подписка на сообщение Lyra.Elimination.Message. На клиенте происходит broadcast сообщения Lyra.AddNotification.SingleKill



B\_SingleKillRelay добавлен в EAS\_BasicShooterAcolades как Client+Server компонент





