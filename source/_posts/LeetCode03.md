
---

layout: leetcode03手写一个生产消费者队列

title: LeetCode03-手写一个生产消费者队列

date: 2023-02-15 22:48:30

tags: LeetCode

categories: Web

description: LeetCode 手写一个生产消费者队列

top: 4

path: /article/leetcode03

abbrlink: 1677333023

---




# LeetCode03手写一个生产消费者队列



~~~java
package org.linlinjava.litemall.core.notify;


import javax.sound.midi.Soundbank;
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;

class Produce implements   Runnable{



    private final BlockingQueue<Integer> queue;

    private int task = 1;
    public Produce(BlockingQueue queue){
        this.queue = queue;
    }

    @Override
    public void run(){
        while(true){
            try{
                System.out.println("生产了一个task"+task);
                queue.put(task);
                task++;
                System.out.println("当前任务数量为"+ queue.size());
                Thread.sleep(1000);
            }catch (Exception ex){
                // do nothing
            }
        }


    }}

class Consumer implements  Runnable{



    private final  BlockingQueue<Integer> queue;

    private int task;
    public Consumer(BlockingQueue queue){
        this.queue = queue;
    }

    @Override
    public void run(){
        while(true){
            try{
                int a= queue.take();
//                task--;
                System.out.println("消费了一个"+ a);
                System.out.println("当前任务数量为"+ queue.size());
                Thread.sleep(2000);
            }catch (Exception ex){
                // do nothing
            }
        }


    }}

class Test{

    public static void main(String[] args){
        ArrayBlockingQueue<Integer> queue  = new ArrayBlockingQueue<>(5);
        Produce prd = new Produce(queue);
        Consumer con =new Consumer(queue);
        Thread t1= new Thread(prd);
        Thread t2 =new Thread(con);
        t1.start();
        t2.start();
    }
}








~~~







