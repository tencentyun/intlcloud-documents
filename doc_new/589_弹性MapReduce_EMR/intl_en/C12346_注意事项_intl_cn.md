1. For the commands above, the source and destination versions must be the same.

2. You may fail to copy the source file if another client is writing data to it; you will fail to rewrite a file if it is being copied to the destination; you will fail to copy the source file if it was being moved, and you will see an error saying FileNotFoundException.