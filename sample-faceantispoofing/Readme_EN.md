English|[中文](Readme.md)

# Face Anti-Spoofing<a name="EN-US_TOPIC_0219080565"></a>

This application can run on the Atlas 200 DK to collect camera data in real time and check the real person through video.

The current application adapts to  [DDK&RunTime](https://ascend.huawei.com/resources)  of 1.31.0.0 and later versions.

## Prerequisites<a name="section137245294533"></a>

Before deploying this sample, ensure that:

-   Mind Studio  has been installed.
-   The Atlas 200 DK developer board has been connected to  Mind Studio, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Software Preparation<a name="section081240125311"></a>

Before running this sample, obtain the source code package, configure the environment, and prepare a model file as follows:

1.  <a name="li953280133816"></a>Obtain the source code package.
    1.  By downloading the package

        Download all the code in the repository at  [https://gitee.com/Atlas200DK/sample-faceantispoofing](https://gitee.com/Atlas200DK/sample-headposeestimation)  to any directory on Ubuntu Server where Mind Studio is located as the Mind Studio installation user, for example,  **$HOME/AscendProjects/sample-faceantispoofing**.

    2.  By running the  **git**  command

        Run the following command in the  **$HOME/AscendProjects**  directory to download code:

        **git clone https://gitee.com/Atlas200DK/sample-faceantispoofing.git --branch 1.3x.0.0**

2.  <a name="li1365682471610"></a>Obtain the source network model required by the application.

    Obtain the source network model and its weight file used in the application by referring to  [Table 1](#table144841813177)  and save them to the same directory on Ubuntu Server where Mind Studio is located, for example,  **$HOME/models/faceantispoofing**.

    **Table  1**  Models used in the face anti-spoofing application

    <a name="table144841813177"></a>
    <table><thead align="left"><tr id="row161061318181712"><th class="cellrowborder" valign="top" width="13.861386138613863%" id="mcps1.2.4.1.1"><p id="p1410671814173"><a name="p1410671814173"></a><a name="p1410671814173"></a>Model Name</p>
    </th>
    <th class="cellrowborder" valign="top" width="24.752475247524753%" id="mcps1.2.4.1.2"><p id="p1106118121716"><a name="p1106118121716"></a><a name="p1106118121716"></a>Description</p>
    </th>
    <th class="cellrowborder" valign="top" width="61.386138613861384%" id="mcps1.2.4.1.3"><p id="p14106218121710"><a name="p14106218121710"></a><a name="p14106218121710"></a>Download Path</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1710661814171"><td class="cellrowborder" valign="top" width="13.861386138613863%" headers="mcps1.2.4.1.1 "><p id="p85671718123118"><a name="p85671718123118"></a><a name="p85671718123118"></a>face_detection</p>
    </td>
    <td class="cellrowborder" valign="top" width="24.752475247524753%" headers="mcps1.2.4.1.2 "><p id="p1456731819318"><a name="p1456731819318"></a><a name="p1456731819318"></a>Network model for face detection.</p>
    <p id="p256717183312"><a name="p256717183312"></a><a name="p256717183312"></a>It is converted from the Caffe-based ResNet10-SSD300 model.</p>
    </td>
    <td class="cellrowborder" valign="top" width="61.386138613861384%" headers="mcps1.2.4.1.3 "><p id="p1956741833120"><a name="p1956741833120"></a><a name="p1956741833120"></a>Download the source network model file and its weight file by referring to<strong id="b1979216239548"><a name="b1979216239548"></a><a name="b1979216239548"></a> README.md</strong> at <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/face_detection" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/face_detection</a>.</p>
    </td>
    </tr>
    <tr id="row8833411314"><td class="cellrowborder" valign="top" width="13.861386138613863%" headers="mcps1.2.4.1.1 "><p id="p65671018123118"><a name="p65671018123118"></a><a name="p65671018123118"></a>depl</p>
    </td>
    <td class="cellrowborder" valign="top" width="24.752475247524753%" headers="mcps1.2.4.1.2 "><p id="p9567131833116"><a name="p9567131833116"></a><a name="p9567131833116"></a>Network model of facial feature points. It is converted from the Caffe-based VGG-SSD model.</p>
    </td>
    <td class="cellrowborder" valign="top" width="61.386138613861384%" headers="mcps1.2.4.1.3 "><p id="p981712263315"><a name="p981712263315"></a><a name="p981712263315"></a>Download the source network model file and its weight file by referring to <strong id="b18659561976"><a name="b18659561976"></a><a name="b18659561976"></a>README.md</strong> at <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/head_pose_estimation" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/head_pose_estimation</a>.</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  Log in to Ubuntu Server where Mind Studio is located as the Mind Studio installation user, determine the current DDK version number, and set the environment variables  **DDK\_HOME**,  **tools\_version**,  **LD\_LIBRARY\_PATH**.
    1.  <a name="li61417158198"></a>Query the current DDK version number.

        A DDK version number can be queried by using either Mind Studio or the DDK software package.

        -   Using Mind Studio

            On the project page of Mind Studio, choose  **File \> Settings \> System Settings \> Ascend DDK**  to query the DDK version number, as shown in  [Figure 1](#fig17553193319118).

            **Figure  1**  Querying the DDK version number<a name="fig17553193319118"></a>  
            ![](figures/querying-the-ddk-version-number-34.png "querying-the-ddk-version-number-34")

            The displayed  **DDK Version**  is the current DDK version number, for example,  **1.31.T15.B150**.

        -   Using the DDK software package

            Obtain the DDK version number based on the DDK package name.

            DDK package name format:  **Ascend\_DDK-\{**_software version_**\}-\{**_interface version_**\}-x86\_64.ubuntu16.04.tar.gz**

            _Software version_  indicates the DDK software version number.

            For example:

            If the DDK package name is  **Ascend\_DDK-1.31.T15.B150-1.1.1-x86\_64.ubuntu16.04.tar.gz**, the DDK version is  **1.31.T15.B150**.

    2.  Set environment variables.

        **vim \~/.bashrc**

        Run the following commands to add the environment variables  **DDK\_HOME**  and  **LD\_LIBRARY\_PATH**  to the last line:

        **export tools\_version=_1.31.X.X_**

        **export DDK\_HOME=\\$HOME/.mindstudio/huawei/ddk/\\$tools\_version/ddk**

        **export LD\_LIBRARY\_PATH=$DDK\_HOME/lib/x86\_64-linux-gcc5.4**

        >![](public_sys-resources/icon-note.gif) **NOTE:**   
        >-   **_1.31.X.X_**  indicates the DDK version queried in  [a](#li61417158198). Set this parameter based on the query result, for example,  **1.31.T15.B150**.  
        >-   If the environment variable has been added, skip this step.  

        Type  **:wq!**  to save settings and exit.

        Run the following command for the environment variable to take effect:

        **source \~/.bashrc**

4.  Convert the source network model to a model supported by the Ascend AI processor.
    1.  Choose  **Tools \> Model Convert**  from the main menu of Mind Studio.
    2.  On the  **Model Conversion**  page that is displayed, configure model conversion.
        -   Select the model file downloaded in  [Step 2](#li1365682471610)  for  **Model File**. The weight file is automatically matched and filled in  **Weight File**.
        -   Set  **Model Name**  to the model name in  [Table 1](#table144841813177).
            1.  On the AIPP configuration page of the face\_detection model, set  **Model Image Format**  to  **BGR888\_U8**. Retain the default values for other parameters.
            2.  The AIPP function must be disabled on the AIPP configuration page of the DEPL model.

    3.  During the conversion, the error information occurs with the face\_detection model, as shown in  [Figure 2](#fig2865313121718).

        **Figure  2**  Model conversion error<a name="fig2865313121718"></a>  
        

        ![](figures/model_facedetection_coversionfailed-35.png)

        Select  **SSDDetectionOutput**  from the  **Suggestion**  drop-down list box at the  **DetectionOutput**  layer and click  **Retry**.

        After successful conversion, an .om offline model is generated in the  **$HOME/modelzoo/xxx/device**  directory.

        >![](public_sys-resources/icon-note.gif) **NOTE:**   
        >For details about the descriptions of each step and parameters in model conversion, see "Model Conversion" in the  [Mind Studio User Guide](https://ascend.huawei.com/doc/mindstudio/).  


5.  Upload the converted .om model file to the  **sample-faceantispoofing/script**  directory under the source code path in  [Step 1](#li953280133816).

## Build<a name="section7994174585917"></a>

1.  Open the project.

    Go to the directory that stores the decompressed installation package as the Mind Studio installation user in CLI mode, for example,  **$HOME/MindStudio-ubuntu/bin**. Run the following command to start Mind Studio:

    **./MindStudio.sh**

    Open the  **sample-faceantispoofing**  project, as shown in  [Figure 3](#fig05481157171918).

    **Figure  3**  Opening the faceantispoofing project<a name="fig05481157171918"></a>  
    

    ![](figures/en-us_image_0219083850.jpg)

2.  Configure project information in the  **src/param\_configure.conf**  file.

    For details, see  [Figure 4](#fig0391184062214).

    **Figure  4**  Configuration file<a name="fig0391184062214"></a>  
    

    ![](figures/en-us_image_0219083915.png)

    Content of the configuration file:

    ```
    remote_host=
    data_source=
    presenter_view_app_name=
    ```

    -   **remote\_host**: IP address of the Atlas 200 DK developer board
    -   **data\_source**: camera channel. The value can be  **Channel-1**  or  **Channel-2**. For details, see "Viewing the Channel to Which a Camera Belongs" in  [Atlas 200 DK User Guide](https://ascend.huawei.com/documentation).
    -   **presenter\_view\_app\_name**: value of  **View Name**  on the  **Presenter Server**  page, which must be unique. The value consists of at least one character and supports only uppercase letters, lowercase letters, digits, and underscores \(\_\).

    Configuration example:

    ```
    remote_host=192.168.1.2
    data_source=Channel-1
    presenter_view_app_name=video
    ```

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   All the three parameters must be set. Otherwise, the build fails.  
    >-   Do not use double quotation marks \(""\) during parameter settings.  

3.  Run the  **deploy.sh**  script to adjust configuration parameters and download and compile the third-party library. Open the  **Terminal**  window of Mind Studio. By default, the home directory of the code is used. Run the  **deploy.sh**  script in the background to deploy the environment, as shown in  [Figure 5](#fig22681517439).

    **Figure  5**  Running the deploy.sh script<a name="fig22681517439"></a>  
    ![](figures/running-the-deploy-sh-script-36.png "running-the-deploy-sh-script-36")

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   During the first deployment, if no third-party library is used, the system automatically downloads and builds the third-party library, which may take a long time. The third-party library can be directly used for the subsequent build.  
    >-   During deployment, select the IP address of the host that communicates with the developer board. Generally, the IP address is the IP address configured for the virtual NIC. If the IP address is in the same network segment as the IP address of the developer board, it is automatically selected for deployment. If they are not in the same network segment, you need to manually type the IP address of the host that communicates with the Atlas DK to complete the deployment.  

4.  Start building. Open Mind Studio and choose  **Build \> Build \> Build-Configuration**  from the main menu. The  **build**  and  **run**  folders are generated in the directory.

    >![](public_sys-resources/icon-notice.gif) **NOTICE:**   
    >When you build a project for the first time,  **Build \> Build**  is unavailable. You need to choose  **Build \> Edit Build Configuration**  to set parameters before the build.  

5.  <a name="li499911453439"></a>Start Presenter Server.

    Open the  **Terminal**  window of Mind Studio. By default, under the code storage path, run the following command to start the Presenter Server program of the face anti-spoofing application on the server,

    **bash run\_present\_server.sh**

    When the message  **Please choose one to show the presenter in browser\(default: 127.0.0.1\):**  is displayed, type the IP address \(usually IP address for accessing Mind Studio\) used for accessing the Presenter Server service in the browser.

    Select the IP address used by the browser to access the Presenter Server service in  **Current environment valid ip list**, as shown in  [Figure 6](#fig999812514814).

    **Figure  6**  Project deployment<a name="fig999812514814"></a>  
    

    ![](figures/en-us_image_0219084084.jpg)

    [Figure 7](#fig69531305324)  shows that the Presenter Server service has been started successfully.

    **Figure  7**  Starting the Presenter Server process<a name="fig69531305324"></a>  
    

    ![](figures/en-us_image_0219085022.jpg)

    Use the URL shown in the preceding figure to log in to Presenter Server \(only Google Chrome is supported\). The IP address is that typed in  [Figure 6](#fig999812514814)  and the default port number is  **7007**. The following figure indicates that Presenter Server has been started successfully.

    **Figure  8**  Home page<a name="fig64391558352"></a>  
    ![](figures/home-page-37.png "home-page-37")

    The following figure shows the IP address used by Presenter Server and  Mind Studio  to communicate with the Atlas 200 DK.

    **Figure  9**  IP address example<a name="fig1881532172010"></a>  
    ![](figures/ip-address-example-38.png "ip-address-example-38")

    In the figure:

    -   The IP address of the Atlas 200 DK developer board is  **192.168.1.2**  \(connected in USB mode\).
    -   The IP address used by Presenter Server to communicate with the Atlas 200 DK is in the same network segment as the IP address of the Atlas 200 DK on the UI Host server. For example:  **192.168.1.223**.
    -   The following describes how to access the IP address \(such as  **10.10.0.1**\) of Presenter Server using a browser. Because Presenter Server and  Mind Studio  are deployed on the same server, you can access  Mind Studio  through the browser using the same IP address. 


## Run<a name="section551710297235"></a>

1.  Run the face anti-spoofing application.

    On the toolbar of Mind Studio, click  **Run**  and choose  **Run \> Run 'sample-faceantispoofing'**. As shown in  [Figure 10](#fig93931954162719), the executable program is running on the developer board.

    **Figure  10**  Application running sample<a name="fig93931954162719"></a>  
    

    ![](figures/en-us_image_0219085391.jpg)

2.  Use the URL displayed upon the start of the Presenter Server service to log in to Presenter Server. For details, see  [Start Presenter Server](#li499911453439).

    Wait for Presenter Agent to transmit data to the server. Click  **Refresh**. When there is data, the icon in the  **Status**  column for the corresponding channel changes to green, as shown in  [Figure 11](#fig113691556202312).

    **Figure  11**  Presenter Server page<a name="fig113691556202312"></a>  
    ![](figures/presenter-server-page-39.png "presenter-server-page-39")

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   For the face anti-spoofing application, Presenter Server supports a maximum of 10 channels at the same time \(each  _presenter\_view\_app\_name_  parameter corresponds to a channel\).  
    >-   Due to hardware limitations, each channel supports a maximum frame rate of 20 fps. A lower frame rate is automatically used when the network bandwidth is low.  

3.  Click a link in the  **View Name**  column, for example,  **video**  in the preceding figure, and view the result.

## Follow-up Operations<a name="section177619345260"></a>

-   Stopping the face anti-spoofing application

    The face anti-spoofing application is running continually after being executed. To stop it, perform the following operation:

    Click the stop button to stop the face anti-spoofing application.  [Figure 12](#fig2182182518112)  shows that the face anti-spoofing application has been stopped.

    **Figure  12**  Stopped the face anti-spoofing application<a name="fig2182182518112"></a>  
    

    ![](figures/en-us_image_0219086288.jpg)

-   Stopping the Presenter Server service

    The Presenter Server service is always in running state after being started. To stop the Presenter Server service for the face anti-spoofing application, perform the following operations:

    On the server with  Mind Studio  installed, run the following command as the  Mind Studio  installation user to check the process of the Presenter Server service corresponding to the face anti-spoofing application:

    **ps -ef | grep presenter | grep faceantispoofing**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-faceantispoofing$ ps -ef | grep presenter | grep faceantispoofing 
     ascend    7701  1615  0 14:21 pts/8    00:00:00 python3 presenterserver/presenter_server.py --app faceantispoofing 
    ```

    In the preceding information,  _7701_  indicates the process ID of the Presenter Server service for the face anti-spoofing application. To stop the service, run the following command:

    **kill -9** _7701_

