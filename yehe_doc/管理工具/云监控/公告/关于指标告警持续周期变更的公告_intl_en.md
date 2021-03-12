To enhance user experience and offer more effective alarm services, we have made the following changes to Tencent Cloud CM’s alarm triggering logic:
1. Change of the meaning of “Last for 1-5 periods”: **Last for n periods** now means an alarm is triggered when **n monitored metrics reach the threshold**. For example, **“Last for 1 period” means an alarm is triggered when 1 monitored metric reaches the threshold. The change may increase the number of alarms you receive. You can modify the parameter based on the new logic.
2. “Last for 0 period” is no longer supported for TencentDB for MySQL, SCF, TencentDB for Redis, or TSF log alarms. If you used the setting for these services, CM will automatically change it to “Last for 1 period”, which means the same as “Last for 0 period” by the old logic.


