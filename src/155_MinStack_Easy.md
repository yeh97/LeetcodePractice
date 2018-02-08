

### Leetcode 155
#### [Min Stack](https://leetcode.com/problems/min-stack)

  

##### ***Problem:***

    Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
    
##### ***Example:***

    Input: ["MinStack","push","push","push","getMin","pop","top","getMin"], [[],[-2],[0],[-3],[],[],[],[]]
        Output: [null,null,null,null,-3,null,0,-2]


##### *Method #1*
``` java
/*
 *Author: yeh
 *Time: 2018_01_30
 *Language: Java
 *
 */

class MinStack {
    // 2018/1/30 : 108ms
    /** initialize your data structure here. */
    Stack<Integer> p = null;
    Stack<Integer> q = null;
    public MinStack() {
        p = new Stack<Integer>();
        q = new Stack<Integer>();
    }
    
    public void push(int x) {
        p.push(x);
        if (q.empty()) {
            q.push(x);
        } else {
            q.push(Math.min(x, q.peek()));
        }
    }
    
    public void pop() {
        p.pop();
        q.pop();
    }
    
    public int top() {
        return p.peek();
    }
    
    public int getMin() {
        return q.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */

```

##### *Method #2*
``` java
/*
 *Author: yeh
 *Time: 2018_01_30
 *Language: Java
 *
 */

class MinStack {
    // 2018/1/30 : 99ms
    /** initialize your data structure here. */
    Stack<Long> p = null;
    long minv;
    public MinStack() {
        p = new Stack<Long>();
    }
    
    public void push(int x) {
        if (p.empty()) {
            p.push((long) 0);
            minv = x;
        } else {
            p.push(x - minv);
            minv = Math.min(minv, x);
        }
    }
    
    public void pop() {
        if (p.empty()) return;
        // p.top() < 0 --> minv will be changed if pop
        if (p.peek() < 0) minv -= p.peek();
        p.pop();
    }
    
    public int top() {
        if (p.empty()) return 0; // err
        if (p.peek() > 0) {
            return (int) (minv + p.peek());
        } else {
            return (int) (minv);
        }
    }
    
    public int getMin() {
        if (p.empty()) return 0; // err
        return (int) (minv);
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */

```

