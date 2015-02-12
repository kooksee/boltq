# boltq
boltq is a very simple boltdb based embedded queue

##usage


```javascript
import (
	"fmt"
	"github.com/oliveagle/boltq"
)

func main() {
	// max_queue_size is 1
	q, err := boltq.NewBoltQ("test_q.queue", 1, boltq.ERROR_ON_FULL)
	defer q.Close()

	q.Enqueue([]byte("value"))
	
	// queue now is full, enqueue another item will raise an error
	err := q.Enqueue([]byte("value"))
	fmt.Println(err)

	// check if queue is full
	isFull := q.IsFull()
	fmt.Println(q.Size() >= q.GetMaxQueueSize())

	// dequeue
	value, _ := q.Dequeue()
	
	// dequeue an empty queue will raise an error
	_, err = q.Dequeue()
	
}
```