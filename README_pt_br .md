# Turtlestein (Turtlebot com Jetson Nano e Ubuntu 20.04)

# Sobre o projeto

Este projeto foi desenvolvido para adaptar uma jetson Nano com ubuntu 20.04, a idéia é que com a Jetson o Turtlebot tenha mais capacidades de trabalhar com mais softwares embarcados, assim tirando um pouco a dependência de estar sempre com um computador conectado. Assim a maioria dos códigos vão ser rodados dentro da Jetson.


# Materiais Utilizados
- Turtlebot3 Waffle Pi
- Jetson Nano
- Bateria
- Sd card 64GB ou mais
- Adaptador Wifi
- Teclado e mouse usb
- Monitor com entrada hdmi


## Turtlebot 3 Waffle Pi

O TurtleBot é um robô de plataforma padrão do ROS. A inspiração para o nome "Turtle" vem de um robô homônimo, que foi impulsionado pela linguagem de programação educacional Logo em 1967. Além disso, o node turtlesim, que aparece pela primeira vez no tutorial básico do ROS, é um programa que simula o sistema de comandos do programa da tartaruga Logo. Ele também é usado para criar o ícone da Tartaruga como um símbolo do ROS. Os nove pontos presentes no logotipo do ROS foram derivados da carapaça posterior da tartaruga. O TurtleBot, que tem sua origem na Tartaruga do Logo, foi projetado para facilitar o ensino para aqueles que estão iniciando no ROS por meio do TurtleBot, bem como para ensinar a linguagem de programação utilizando o Logo. Desde então, o TurtleBot se tornou a plataforma padrão do ROS, a mais popular entre desenvolvedores e estudantes.

O TUrtlebot 3 tem 3 versões. o Burger, o Waffle e o Waffle Pi. Vamos utilizar o Waffle Pi


## Jetson Nano

Jetson Nano é uma placa que funciona como um computador de bolso capaz de várias aplicações principalmente com redes neurais e IA. 


### Especificações técnicas


GPU:  Arquitetura NVIDIA Maxwell™ com 128 NVIDIA CUDA® cores

CPU:  Processador Quad-core ARM® Cortex®-A57 MPCore

Memória:  4 GB 64-bit LPDDR4

Armazenamento:  16 GB eMMC 5.1 Flash

Video Encode:  4K @ 30 (H.264/H.265)

Video Decode:  4K @ 60 (H.264/H.265)

Câmera:  12 lanes (3x4 or 4x2) MIPI CSI-2 DPHY 1.1 (18 Gbps)

Conectividade:  Gigabit Ethernet

Visor: HDMI 2.0 ou DP1.2 | eDP 1.4 | 2 DSI simultâneos (1 x2)

UPHY: 1 x1/2/4 PCIE, 1x USB 3.0, 3x USB 2.0

I/O: 1x SDIO / 2x SPI / 4x I2C / 2x I2S / GPIOs -> I2C, I2S

Dimensões: 69.6 mm x 45 mm

Mecânico: Conector de ponta com 260 pinos


## Bateria

A bateria usada foi a NH2054 da Inspired Energy, é uma bateria de 14.4 V com 6.2 Ah. Essa bateria foi escolhida para ter mais tempo de uso sem necessidade de recarregar varias vezes. Mas para usar uma bateria dessas foi necessário ter um regulador de 5 Volts para alimentar a Jetson. 

### Bateria Frontal

![Bateria_Frontal](https://github.com/MarcuSpade/Turtlestein/blob/main/Assets/Bateria_frontal.jpeg)


### Bateria Traseiro

![bateria_traseira](https://github.com/MarcuSpade/Turtlestein/blob/main/Assets/Bateria_verso.jpeg)

### Regulador de Tesnsão de 5 V

![Regulador_de_tensao](https://github.com/MarcuSpade/Turtlestein/blob/main/Assets/regulador_tensao.jpeg)


## Adaptador Wifi

Usei um adaptador genérico modelo ka-t8188, foi bem difícil achar o driver dele para funcionar no Ubuntu 20.04, mas consegui achar no github do [@kelebek333](https://github.com/kelebek333), vou deixar o link do github dele mostrando toda a configuração para esse adaptador.

https://github.com/kelebek333/rtl8188fu


## Cartão SD

É importante um cartão SD de 64 GB ou mais, só o sistema consome 27 GB de armazenamento.


# Instruções

## Configuração da Jetson

A Jetson por fábrica só tem acesso ao Ubuntu 18.04, porém graças ao [Qengineering](https://github.com/Qengineering) que desenvolveu uma nova imagem para o Jetson, temos acesso ao Ubuntu 20.04, por isso vou deixar abeixo o link do github dele.

https://github.com/Qengineering/Jetson-Nano-Ubuntu-20-image


- Você vai baixar a imagem nesse [link](https://ln5.sync.com/dl/f65071870/b5vp32ch-8s23cgn4-b9e4w24q-i2sf9aw2/view/default/13150797710004)
- Fazer um flash no sdcard com o [balenaEtcher](https://etcher.balena.io/#download-etcher)
- Conectar o sdcard na Jetson
- Conectar um monitor no hdmi, e um teclado e mouse usb.
- Conectar a Jetson a Internet via cabo ou fazendo o passo a passo para usar o adaptador wifi

![Jetson_Ubuntu](https://github.com/MarcuSpade/Turtlestein/blob/main/Assets/jetson_ubuntu2004.jpeg)


### Instalação do ROS2 e pacotes

As Instruções abaixo foram adaptadas do passo a passo do Turtlebot3 disponível no site da [Robotis](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/) , se você quiser fazer o passo a passo por lá, pode fazer. Porém lembre que o objetivo é que o código seja rodado completamente embarcado, sendo assim, o passo a passo tanto do [PC_Setup](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup) quanto o do [SBC_Setup](https://emanual.robotis.com/docs/en/platform/turtlebot3/sbc_setup/#sbc-setup) será feito na Jetson

#### Instalação do ROS2 Foxy

O Ubuntu 20.04 só permite a instalação do ROS2 FOXY, sendo assim vamos instalar ele, tentei instalar a versão direto do site oficial do ROS porém não consegui instalar na Jetson então instalei a versão da Robotis mesmo.

    wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros2_foxy.sh
    sudo chmod 755 ./install_ros2_foxy.sh
    bash ./install_ros2_foxy.sh

#### Instalação dos pacotes do ROS2 e Turtlebot3

    sudo apt install ros-foxy-cartographer
    sudo apt install ros-foxy-cartographer-ros
    sudo apt install ros-foxy-navigation2
    sudo apt install ros-foxy-nav2-bringup
    sudo apt install ros-foxy-dynamixel-sdk
    sudo apt install ros-foxy-turtlebot3-msgs
    sudo apt install ros-foxy-turtlebot3
    sudo apt install python3-argcomplete python3-colcon-common-extensions libboost-system-dev build-essential
    sudo apt install ros-foxy-hls-lfcd-lds-driver
    mkdir -p ~/turtlebot3_ws/src && cd ~/turtlebot3_ws/src
    git clone -b foxy-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
    cd ~/turtlebot3_ws/
    echo 'source /opt/ros/foxy/setup.bash' >> ~/.bashrc
    source ~/.bashrc
    colcon build --symlink-install --parallel-workers 1
    echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc
    source ~/.bashrc
    
#### Configuração Driver LDS

Existem duas versões de Sensor LDS para o Turlebot3, os modelos a partir do ano de 2022 vem com o modelo LDS-02, então veja se você está com o modelo LDS-01 ou o LDS-02

##### LDS-01

![LDS_01](https://emanual.robotis.com/assets/images/platform/turtlebot3/appendix_lds/lds_small.png)

##### LDS-02

![LDS_02](https://emanual.robotis.com/assets/images/platform/turtlebot3/appendix_lds/lds_ld08_small.png)

Se você está utilizando o LDS-01 só precisa exportar o modelo para o .bashrc

    echo 'export LDS_MODEL=LDS-02' >> ~/.bashrc
    source ~/.bashrc

Se está usando o LDS-02 deve instalar o drive dele

    sudo apt update
    sudo apt install libudev-dev
    cd ~/turtlebot3_ws/src
    git clone -b ros2-devel https://github.com/ROBOTIS-GIT/ld08_driver.git
    cd ~/turtlebot3_ws/src/turtlebot3 && git pull
    cd ~/turtlebot3_ws && colcon build --symlink-install

### Configuração de Ambiente

    echo 'export ROS_DOMAIN_ID=30 #TURTLEBOT3' >> ~/.bashrc
    source ~/.bashrc

### Configuração OpenCR

Para fazer essa configuração é necessário conectar o OpenCR ao Jetson via cabo microUSB

![montagem_jetson](https://github.com/MarcuSpade/Turtlestein/blob/main/Assets/WhatsApp%20Image%202023-08-10%20at%2015.46.54.jpeg)

    sudo cp `ros2 pkg prefix turtlebot3_bringup`/share/turtlebot3_bringup/script/99-turtlebot3-cdc.rules /etc/udev/rules.d/
    sudo udevadm control --reload-rules
    sudo udevadm trigger

Instale os pacotes para fazer o upload do firmware

    sudo dpkg --add-architecture armhf
    sudo apt update
    sudo apt install libc6:armhf

Dependendo da plataforma use burger ou waffle para o OPENCR_MODEL

    export OPENCR_PORT=/dev/ttyACM0
    export OPENCR_MODEL=burger
    rm -rf ./opencr_update.tar.bz2

Faça o download do firmware e loader, depois extraia o arquivo

    wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS2/latest/opencr_update.tar.bz2
    tar -xvf ./opencr_update.tar.bz2

Faça o upload do firmware do OpenCR

    cd ~/opencr_update
    ./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr

Se tudo der certo seu terminal deve ficar parecido com a imagem abaixo.

![update_OpenCR](https://emanual.robotis.com/assets/images/platform/turtlebot3/opencr/shell01.png)


## Montagem

Para realizar a montagem é só seguir o passo a passo que está no site da [Robotis](https://emanual.robotis.com/docs/en/platform/turtlebot3/hardware_setup/)

Abaixo uma foto da placa montada na estrutura

![placa_montada](https://github.com/MarcuSpade/Turtlestein/blob/main/Assets/WhatsApp%20Image%202023-08-10%20at%2015.46.54.jpeg)


