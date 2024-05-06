# Dockerでのシミュレーション環境のセットアップ

RoboticaUtnFrba/create_autonomyのリポジトリにおいてルンバのROS1のgazebo環境が提供されていたが、ROS2はサポートされていないため、代替としてturtlebot3のシミュレーション環境を使用する。

## 1. Docker ROS2 Humbleのセットアップ

1. DockerDesktopをインストールする。
2. Tiryoh氏の[docker-ros2-desktop-vnc](https://github.com/Tiryoh/docker-ros2-desktop-vnc) のQuick Startに従ってUbuntu Desktop + ROS2 Humble環境を起動する。

## 2. Gazeboシミュレーターのセットアップ

1. 以下のパッケージをインストールする
    ```
    sudo apt update
    sudo apt -y install ros-humble-gazebo-ros-pkgs
    sudo apt -y install ros-humble-dynamixel-sdk
    sudo apt -y install ros-humble-turtlebot3-msgs
    sudo apt -y install ros-humble-turtlebot3
    ```
1. turtlebot3のシミュレーション環境を設定する。
    ```
    mkdir -p ~/colcon_ws/src
    cd ~/colcon_ws/src/
    git clone -b humble-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
    cd ~/colcon_ws && colcon build --symlink-install
    ```
1. bashrcを設定する。
    ```
    echo "source ~/colcon_ws/install/local_setup.bash" >> ~/.bashrc
    echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
    source ~/.bashrc
    ```

## 3. Gazeboシミュレーターの起動

1. 新たにターミナルを起動して以下のコマンドを入力する。
    ```
    ros2 launch turtlebot3_gazebo empty_world.launch.py
    ```
1. もう一つターミナルを起動（右クリックで画面分割ができる）して以下のコマンドを入力する。
    ```
    ros2 run turtlebot3_teleop teleop_keyboard
    ```
1. キーボードでシミュレータのturtlebot(Roomba)がコントロールできることを確認する。

## 参考サイト
Robotis e-manual turtlebot3  
https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/

RoboticaUtnFrba/create_autonomy  
https://github.com/RoboticaUtnFrba/create_autonomy