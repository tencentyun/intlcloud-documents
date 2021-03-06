スケーリング処理取消とは、定時タスクが開始またはアラームスケーリングの条件が達成し、スケーリング処理がトリガーされたが、コンフリクトが存在するため、スケーリング処理がキャンセルされました。

**コンフリクトの原因：**
- ほかのスケーリング処理が実行中
- スケーリンググループがクールダウン時間中

**スケーリング処理がキャンセルされた後、リトライされますか？**
- **アラームスケーリング** 処理がキャンセルされた場合、リトライされません。ただし、アラームスケーリングの条件が成立し続けると、次のアラームスケーリング処理がトリガーされます。
- **定時タスク** 期待するインスタンス数、最大スケーリング数、最小スケーリング数が定義されたため、スケーリンググループは実際のインスタンス数が期待するインスタンス数に満たすようにリトライし続けます。

>一時中止されたスケーリンググループがスケーリング処理をリトライしないため、「スケーリング処理」の履歴にキャンセルのスケーリング処理は記録されません。
