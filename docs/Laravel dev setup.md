# Laravel dev setup

there are two options you can choose from

1. Develop on your local windows machine
2. Develop on Ubuntu virtual server

## Develop on Ubuntu virtual server

first connect to wireguard vpn, then you can access the server terminal with VMware ESXi web portal with vmrc or with ssh, instructions below will assume you have access to terminal, if you have difficauly doing so, you can contact me personally.

### First time setup

1. clone the repository

    !!! note

        if you will be pushing code to the remote repository (which you should be) you should consider cloning with ssh instead of https, [see here to configure cloning with ssh key](./github%20ssh%20key%20setup.md)

    with https

        git clone https://github.com/stanly0726/nuu-sign-doc-online.git

    or use ssh

        git clone git@github.com:stanly0726/nuu-sign-doc-online.git

2. cd into directory

        cd nuu-sign-doc-online

3. install php dependencies

        composer i

4. install node dependencies

        npm install

5. copy .env.example to .env

        cp .env.example .env

6. generate new application key

        php artisan key:generate

## Spining up dev server

to start dev server we have to spin up two parts, **laravel** itself and [**vite dev server**](https://laravel.com/docs/10.x/vite)

these two servers defaults to only serve on *localhost* meaning that you cant access it when working remotely, but there're two work arounds(just pick one of them)

since we need to run two command simultaneously, you can open two terminal on your computer and run ssh on both of them or you can use [tmux](https://johnliu55.tw/tmux.html) if your comfortable with it, not going into too much detail here

### ssh tunnel

>[detail information on ssh tunnel](https://johnliu55.tw/ssh-tunnel.html)

1. start both server to see which port they are running on

        php artisan serve

    and

        npm run dev
    
    just look at the outputs to identify the ports

run this command on *your computer*, **not** on *Ubuntu server*
what it does is when you send a request to your computer at port X, it will forward that request to the server at port Y, the ports might not be the same as shown here.

```bash
# ssh -L X:localhost:Y
ssh -L 5173:localhost:5173 -L 8000:localhost:8000 <your_username>@192.168.0.119
```

then you should be able to see the webpage with browser on your computer at <http://localhost:8000>

### expose servers with ip

1. start laravel server with
        
        php artisan serve --host=192.168.0.119

2. modify startup script for vite dev server

    open `package.json` and modify the script for `dev` to

    ```json
    "dev": "vite --host"
    ```

3. start vite dev server

        npm run dev

now you should be able to see the webpage with browser on your computer at <http://192.168.0.119:8000>

## Develop on your local windows machine

1. download laragon
2. you might need you upgrade php or node
3. steps are pretty similar with linux, **use the terminal that comes with laragon**
