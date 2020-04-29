

#  RouterOS 設定流程

1. 標記介面名稱

   ![CleanShot 2020-04-26 at 11.05.24](https://i.imgur.com/Tjfd9NO.png)

   對介面命名，以利後續辨別

   ![CleanShot 2020-04-26 at 11.06.36](https://i.imgur.com/rRQiVg2.png)

   

2. WAN設定PPPoE撥號
   Interface > PPPoE Client 

   ![image-20200426110858458](https://i.imgur.com/rP5E9he.png)

   選擇撥號介面，本例是選擇WAN

   ![CleanShot 2020-04-26 at 11.10.17](https://i.imgur.com/JKRIwDq.png)

   不選 Use Peer DNS

   Add Default Route

   ![CleanShot 2020-04-26 at 11.11.44](https://i.imgur.com/az8u0H4.png)

3. 設定NAT

   IP > Firewall > NAT

   - Chain: scrnat

   - Action: masquerade

     ![CleanShot 2020-04-26 at 11.13.10](https://i.imgur.com/NuuC6XZ.png)

     ![CleanShot 2020-04-26 at 11.13.49](https://i.imgur.com/tRfVH0N.png)![CleanShot 2020-04-26 at 11.14.33](https://i.imgur.com/z6fp5Hg.png)

4. 設定DNS

   IP > DNS

   Allow Remote Request

   ![CleanShot 2020-04-26 at 11.15.15](https://i.imgur.com/wW1pNkr.png)

   ![CleanShot 2020-04-26 at 11.16.17](https://i.imgur.com/lzf5rgU.png)

5. 把LAN埠都橋接在一起

   新增一個Bridge

   ![CleanShot 2020-04-26 at 11.16.50](https://i.imgur.com/VtsaCIn.png)

   把LAN都接在這個Bridge上(Bridge>Ports)，一個一個加

   把LAN1~LAN3加入到bridge內

   ![CleanShot 2020-04-26 at 11.18.02](https://i.imgur.com/eOcRw4V.png)

   ![CleanShot 2020-04-26 at 11.19.27](https://i.imgur.com/M7679sD.png)

6. DHCP server

   1. IP > DHCP server

      ![CleanShot 2020-04-26 at 11.21.12](https://i.imgur.com/o91Dn8m.png)

   2. IP > Pool 新增Address Pool

      ![CleanShot 2020-04-26 at 11.21.52](https://i.imgur.com/ZaPy7v4.png)

      設定DHCP配發IP的範圍

      ![CleanShot 2020-04-26 at 11.22.43](https://i.imgur.com/RMDNrFW.png)

   3. DHCP server > Add > 應用在Bridge上

      ![CleanShot 2020-04-26 at 11.25.10](https://i.imgur.com/cX02Z67.png)

   4. DHCP server > Networks (DHCP配發的設定值都在這)

      ![CleanShot 2020-04-26 at 11.26.09](https://i.imgur.com/wAoDK68.png)

      上面所設定的資料就會對應該各DHCP client接收到的內容

      ![image-20200426112808736](https://i.imgur.com/cebBeS1.png)