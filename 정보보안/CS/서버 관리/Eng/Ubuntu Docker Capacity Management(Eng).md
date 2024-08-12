
![](https://velog.velcdn.com/images/tkops365/post/f03cd953-edc3-4ae4-8b00-60576cf465e8/image.png)


We encountered a difficult error while using Docker at work. The 4TB allocated to Ubuntu was insufficient, so the existing service was down. At first, we thought we could deal with it by deleting files or logs that were taking up a lot of space, but that wasn't the fundamental problem.

Since I spent a lot of time on this issue, I decided to share my solution for developers like me, especially those who develop and maintain Docker servers like me.

# 1. Errors that occur
![](https://velog.velcdn.com/images/tkops365/post/72458452-fa5d-43e7-8f4b-c01625fdce7d/image.png)

When using Docker, you may see that disk usage suddenly increases. Then, you enter the Docker container and check the capacity of the db or the files in the container, but you cannot find the cause.

Why is that?

The reason is simple.

**This is because containers share disk volumes, and garbage data values ​​from the server accumulate on those disk volumes for a long time.**

It is mainly accumulated in the server container that handles logic, but if left for a long time, it will also accumulate in other auxiliary containers such as databases.

* I also had a ton of garbage accumulated in mariaDB, nginx, Grafana, phpadmin, etc.

To put it simply, the cause is that the volumes of deleted or unused images or containers have piled up, creating this situation.

<span style="color: red">What should be done in this situation?

For times like this, Docker has prepared commands.

It is **docker system prun**e .

First, let me explain the method. </span>
  
  
  ```
docker ps -a 
```

First, check the currently running containers with the above command and select containers with large capacity.

(In fact, if the server's capacity is insufficient, all containers are in trouble.)

Then the
```
docker stop <container_id>

---------------------------------

All containers are stopped

docker stop all
```
  
Stop the container with the above command.
  
Then delete the container with the command below.
  
```
docker rm <container_id>
----------------------------------
Delete all containers

docker rm $(docker ps -a -q)
```
  
This part will only mention the commands. (Usually it is not necessary. Run it when there is no change in capacity -> But be careful to delete only unused images.)

Check all existing images:
  
```
docker images
```
  
Delete a specific image:
  
```
docker rmi $(docker images -q)

```
Next, it's time to delete any unused data from Docker.

Delete unused volumes:
  
```
docker volume prune
```
  
Delete all unused containers, images, volumes, and networks:
  
```
docker system prune -a
```
Re-creating and running containers to fulfill the above assumptions would provide a dramatic increase in capacity.

I got 3 terabytes.

Normally, you can just use the docker volume prune command to delete the above volume, but I had to deal with capacity issues again in less than 3 months when I did that the first time I tried.

So docker system prune -a to delete unused images, volumes, containers, networks, etc.

was used.

Of course, I'm not saying you should always use that command, because you never know what problems might arise.
  
<span style="color: yellow">I hope that you won't have any problems with capacity when using Docker on Ubuntu using this method. It was a meaningful event to learn again that volume management is important.</span>