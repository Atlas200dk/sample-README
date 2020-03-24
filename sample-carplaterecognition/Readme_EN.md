English|[中文](Readme.md)

# License Plate Recognition<a name="EN-US_TOPIC_0218873008"></a>

This application can run on the Atlas 200 DK to collect camera data in real time and predict vehicle license plate information in the video. The precision is low due to the model. To improve the precision, you can train a model to replace it.

The applications in the current version branch adapt to  [DDK&RunTime](https://ascend.huawei.com/resources) **1.32.0.0 and later**.

## Prerequisites<a name="section137245294533"></a>

Before deploying this sample, ensure that:

-   Mind Studio  has been installed.
-   The Atlas 200 DK developer board has been connected to  Mind Studio, the cross compiler has been installed, the SD card has been prepared, and basic information has been configured.

## Software Preparation<a name="section8534138124114"></a>

Before running the sample, obtain the source code package and configure the environment as follows:

1.  <a name="li953280133816"></a>Obtain the source code package.
    1.  By downloading the package

        Download all the code in the repository at  [https://gitee.com/Atlas200DK/sample-carplaterecognition/tree/1.3x.0.0/](https://gitee.com/Atlas200DK/sample-carplaterecognition/tree/1.3x.0.0/)  to any directory on Ubuntu Server where Mind Studio is located as the Mind Studio installation user, for example,  **$HOME/AscendProjects/sample-carplaterecognition**.

    2.  By running the  **git**  command

        Run the following command in the  **$HOME/AscendProjects**  directory to download code:

        **git clone https://gitee.com/Atlas200DK/sample-carplaterecognition.git --branch 1.3x.0.0**

2.  <a name="li8221184418455"></a>Obtain the source network model required by the application.

    Obtain the source network model and its weight file used in the application by referring to  [Table 1](#table117203103464)  and save them to the same directory on Ubuntu Server where  Mind Studio  is located, for example,  **$HOME/models/carplaterecognition**.

    **Table  1**  Models used in the license plate recognition application

    <a name="table117203103464"></a>
    <table><thead align="left"><tr id="row4859191074617"><th class="cellrowborder" valign="top" width="17%" id="mcps1.2.4.1.1"><p id="p18859111074613"><a name="p18859111074613"></a><a name="p18859111074613"></a>Model Name</p>
    </th>
    <th class="cellrowborder" valign="top" width="26%" id="mcps1.2.4.1.2"><p id="p17859171013469"><a name="p17859171013469"></a><a name="p17859171013469"></a>Description</p>
    </th>
    <th class="cellrowborder" valign="top" width="56.99999999999999%" id="mcps1.2.4.1.3"><p id="p1385991094614"><a name="p1385991094614"></a><a name="p1385991094614"></a>Download Path</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1985913103461"><td class="cellrowborder" valign="top" width="17%" headers="mcps1.2.4.1.1 "><p id="p14859151016464"><a name="p14859151016464"></a><a name="p14859151016464"></a>car_plate_detection</p>
    </td>
    <td class="cellrowborder" valign="top" width="26%" headers="mcps1.2.4.1.2 "><p id="p108593100461"><a name="p108593100461"></a><a name="p108593100461"></a>Network model for identifying the license plate.</p>
    <p id="p1785921024614"><a name="p1785921024614"></a><a name="p1785921024614"></a>It is a MobileNet-SSD model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.99999999999999%" headers="mcps1.2.4.1.3 "><p id="p158596106460"><a name="p158596106460"></a><a name="p158596106460"></a>Download the source network model file and its weight file by referring to <strong id="b1818472518513"><a name="b1818472518513"></a><a name="b1818472518513"></a>README.md</strong> at <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/car_plate_detection" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/car_plate_detection</a>.</p>
    </td>
    </tr>
    <tr id="row08596101464"><td class="cellrowborder" valign="top" width="17%" headers="mcps1.2.4.1.1 "><p id="p178591510164619"><a name="p178591510164619"></a><a name="p178591510164619"></a>car_plate_recognition</p>
    </td>
    <td class="cellrowborder" valign="top" width="26%" headers="mcps1.2.4.1.2 "><p id="p1485911105469"><a name="p1485911105469"></a><a name="p1485911105469"></a>Network model for identifying the license plate number.</p>
    <p id="p17859191018468"><a name="p17859191018468"></a><a name="p17859191018468"></a>It is a CNN model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.99999999999999%" headers="mcps1.2.4.1.3 "><p id="p7859181094619"><a name="p7859181094619"></a><a name="p7859181094619"></a>Download the source network model file and its weight file by referring to <strong id="b73161446551"><a name="b73161446551"></a><a name="b73161446551"></a>README.md</strong> at <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/classification/car_plate_recognition" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/classification/car_plate_recognition</a>.</p>
    </td>
    </tr>
    <tr id="row88591310124617"><td class="cellrowborder" valign="top" width="17%" headers="mcps1.2.4.1.1 "><p id="p685911013465"><a name="p685911013465"></a><a name="p685911013465"></a>vgg_ssd</p>
    </td>
    <td class="cellrowborder" valign="top" width="26%" headers="mcps1.2.4.1.2 "><p id="p1786011016461"><a name="p1786011016461"></a><a name="p1786011016461"></a>Network model for object detection.</p>
    <p id="p086018109465"><a name="p086018109465"></a><a name="p086018109465"></a>It is an SSD512 model based on Caffe.</p>
    </td>
    <td class="cellrowborder" valign="top" width="56.99999999999999%" headers="mcps1.2.4.1.3 "><p id="p1186071044613"><a name="p1186071044613"></a><a name="p1186071044613"></a>Download the source network model file and its weight file by referring to <strong id="b469184117518"><a name="b469184117518"></a><a name="b469184117518"></a>README.md</strong> at <a href="https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/vgg_ssd" target="_blank" rel="noopener noreferrer">https://gitee.com/HuaweiAscend/models/tree/master/computer_vision/object_detect/vgg_ssd</a>.</p>
    </td>
    </tr>
    </tbody>
    </table>

3.  Log in to Ubuntu Server where Mind Studio is located as the Mind Studio installation user, determine the current DDK version number, and set the environment variables  **DDK\_HOME**,  **tools\_version**,  **LD\_LIBRARY\_PATH**.
    1.  <a name="en-us_topic_0203223294_li61417158198"></a>Query the current DDK version number.

        A DDK version number can be queried by using either Mind Studio or the DDK software package.

        -   Using Mind Studio

            On the project page of Mind Studio, choose  **File \> Settings \> System Settings \> Ascend DDK**  to access  [Querying the DDK version number](#en-us_topic_0203223294_fig17553193319118).

            **Figure  1**  Querying the DDK version number<a name="en-us_topic_0203223294_fig17553193319118"></a>  
            ![](figures/querying-the-ddk-version-number.png "querying-the-ddk-version-number")

            The displayed  **DDK Version**  is the current DDK version number, for example,  **1.31.T15.B150**.

        -   Using the DDK software package

            Obtain the DDK version number based on the DDK package name.

            DDK package name format:  **Ascend\_DDK-\{software version\}-\{interface version\}-x86\_64.ubuntu16.04.tar.gz**

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
        >-   **_1.31.X.X_**  indicates the DDK version queried in  [a](#en-us_topic_0203223294_li61417158198). Set this parameter based on the query result, for example,  **1.31.T15.B150**.  
        >-   If the environment variables have been added, skip this step.  

        Type  **:wq!**  to save settings and exit.

        Run the following command for the environment variable to take effect:

        **source \~/.bashrc**

4.  Convert the source network model to a model supported by the Ascend AI processor. A model can be converted either using Mind Studio or in CLI mode.
    -   Convert a model using Mind Studio.
        1.  Choose  **Tools \> Model Convert**  from the main menu of Mind Studio.
        2.  On the  **Model Conversion**  page that is displayed, configure model conversion.
            -   Select the model file downloaded in  [Step 2](#li8221184418455)  for  **Model File**. The weight file is automatically matched and filled in  **Weight File**.
            -   Set  **Model Name**  to the model name in  [Table 1](#table117203103464).
            -   Set the following parameters for car\_plate\_detection model conversion:

                In the  **AIPP**  configuration, change the values of  **Input Image Size**  to  **512**  and  **640**  respectively. The values must be 128 x 16 aligned. Select  **BGR888\_U8**  for  **Model Image Format**.

            -   Set the following parameters for car\_plate\_recognition model conversion:

                In the  **AIPP**  configuration, change the values of  **Input Image Size**  to  **384**  and  **80**  respectively. The values must be 128 x 16 aligned. Select  **BGR888\_U8**  for  **Model Image Format**.

            -   Set the following parameters for vgg\_ssd model conversion:

                Select  **BGR888\_U8**  for  **Model Image Format**.

        3.  Click  **OK**  to start model conversion.

            During the conversion of the  **car\_plate\_detection**  and** vgg\_ssd**  models, the following error will be reported.

            **Figure  2**  Model conversion error<a name="fig1842765585311"></a>  
            

            ![](figures/model_facedetection_coversionfailed-25.png)

            Select  **SSDDetectionOutput**  from the  **Suggestion**  drop-down list box at the  **DetectionOutput**  layer and click  **Retry**.

            After successful conversion, an .om offline model is generated in the  **$HOME/modelzoo/xxx/device**  directory.

            >![](public_sys-resources/icon-note.gif) **NOTE:**   
            >-   For details about the descriptions of each step and parameters in model conversion on Mind Studio, see "Model Conversion" in the  [Mind Studio User Guide](https://ascend.huawei.com/doc/mindstudio/).  
            >-   **xxx**  indicates the name of the model to be converted. For example,  **vgg\_ssd.om**  is stored in  **$HOME/modelzoo/vgg\_ssd/device**.  


    -   Convert a model in CLI mode.
        1.  Go to the folder for storing source models as the Mind Studio installation user.

            **cd $HOME/models/carplaterecognition**

        2.  Run the following command to convert the model using OMG:

            ```
            ${DDK_HOME}/uihost/bin/omg --output="./XXX" --model="./XXX.prototxt" --framework=0 --ddk_version=${tools_version} --weight="./XXX.caffemodel" --input_shape=`head -1 $HOME/AscendProjects/sample-carplaterecognition/script/shape_XXX` --insert_op_conf=$HOME/AscendProjects/sample-carplaterecognition/script/aipp_XXX.cfg --op_name_map=$HOME/AscendProjects/sample-carplaterecognition/script/reassign_operators
            ```

            >![](public_sys-resources/icon-note.gif) **NOTE:**   
            >-   The files required by  **input\_shape**,  **insert\_op\_conf**, and  **op\_name\_map**  are stored in the  **sample-carplaterecognition/script**  directory under the source code path. Configure the file paths based on the actual source code path.  
            >-   **XXX**  indicates the name of the model used in  [Table 1](#table117203103464). Replace it with the name of the model to be converted. The  **op\_name\_map**  parameter is not required during  **car\_plate\_recognition**  model conversion. If unnecessary parameters are not deleted, an error is reported during model conversion.  
            >-   For details about parameter descriptions, see "Model Conversion" in the  [Atlas 200 DK User Guide](https://ascend.huawei.com/doc/atlas200dk/).  


5.  Upload the converted .om model file to the  **sample-carplaterecognition/script**  directory in the source code path in  [Step 1](#li953280133816).

## Build<a name="section1759513564117"></a>

1.  Open the project.

    Go to the directory that stores the decompressed installation package as the Mind Studio installation user in CLI mode, for example,  **$HOME/MindStudio-ubuntu/bin**. Run the following command to start Mind Studio:

    **./MindStudio.sh**

    Open the  **sample-carplaterecognition**  project, as shown in  [Figure 3](#fig721144422212).

    **Figure  3**  Opening the sample-carplaterecognition project<a name="fig721144422212"></a>  
    

    ![](figures/en-us_image_0218876987.png)

2.  Configure project information in the  **src/param\_configure.conf**  file.

    **Figure  4**  Configuration file path<a name="fig1557065718252"></a>  
    

    ![](figures/en-us_image_0218877806.png)

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

3.  Run the  **deploy.sh**  script to adjust configuration parameters and download and compile the third-party library. Open the  **Terminal**  window of Mind Studio. By default, the home directory of the code is used. Run the  **deploy.sh**  script in the background to deploy the environment, as shown in  [Figure 5](#fig19393122943511).

    **Figure  5**  Running the deploy.sh script<a name="fig19393122943511"></a>  
    ![](figures/running-the-deploy-sh-script-26.png "running-the-deploy-sh-script-26")

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   During the first deployment, if no third-party library is used, the system automatically downloads and builds the third-party library, which may take a long time. The third-party library can be directly used for the subsequent build.  
    >-   During deployment, select the IP address of the host that communicates with the developer board. Generally, the IP address is the IP address configured for the virtual NIC. If the IP address is in the same network segment as the IP address of the developer board, it is automatically selected for deployment. If they are not in the same network segment, you need to manually type the IP address of the host that communicates with the Atlas DK to complete the deployment.  

4.  Start building. Open Mind Studio and choose  **Build \> Build \> Build-Configuration**  from the main menu. The  **build**  and  **run**  folders are generated in the directory, as shown in  [Figure 6](#fig13819202814301).

    **Figure  6**  Build and file generation<a name="fig13819202814301"></a>  
    

    ![](figures/977f70e5b743c8ab6267c7d9b93194c.png)

    >![](public_sys-resources/icon-notice.gif) **NOTICE:**   
    >When you build a project for the first time,  **Build \> Build**  is unavailable. You need to choose  **Build \> Edit Build Configuration**  to set parameters before the build.  

5.  <a name="li499911453439"></a>Start Presenter Server.

    Open the  **Terminal**  window of Mind Studio. Under the code storage path, run the following command to start the Presenter Server program of the license plate recognition application on the server, as shown in  [Figure 7](#fig102142024389).

    **bash run\_present\_server.sh**

    **Figure  7**  Starting Presenter Server<a name="fig102142024389"></a>  
    

    ![](figures/3510ef898c672612c4ac5fa9397c708.png)

    -   When the message  **Please choose one to show the presenter in browser\(default: 127.0.0.1\):**  is displayed, type the IP address \(usually IP address for accessing Mind Studio\) used for accessing the Presenter Server service in the browser.

        Select the IP address used by the browser to access the Presenter Server service in  **Current environment valid ip list**  and type the path for storing video analysis data, as shown in  [Figure 8](#fig73590910118).

        **Figure  8**  Project deployment<a name="fig73590910118"></a>  
        

        ![](figures/827447f108867314d18ff4e4b22d421.png)

    [Figure 9](#fig19953175965417)  shows that the Presenter Server service has been started successfully.

    **Figure  9**  Starting the Presenter Server process<a name="fig19953175965417"></a>  
    

    ![](figures/de3f85cb841628787ec4718cee44e8e.png)

    Use the URL shown in the preceding figure to log in to Presenter Server \(only Google Chrome is supported\). The IP address is that typed in  [Project deployment](#fig73590910118)  and the default port number is  **7007**. The following figure indicates that Presenter Server has been started successfully.

    **Figure  10**  Home page<a name="fig64391558352"></a>  
    ![](figures/home-page-27.png "home-page-27")

    The following figure shows the IP address used by Presenter Server and  Mind Studio  to communicate with the Atlas 200 DK.

    **Figure  11**  IP address example<a name="fig195318596543"></a>  
    ![](figures/ip-address-example-28.png "ip-address-example-28")

    -   The IP address of the Atlas 200 DK developer board is  **192.168.1.2**  \(connected in USB mode\).
    -   The IP address used by Presenter Server to communicate with the Atlas 200 DK is in the same network segment as the IP address of the Atlas 200 DK on the UI Host server. For example:  **192.168.1.223**.
    -   The following describes how to access the IP address \(such as  **10.10.0.1**\) of Presenter Server using a browser. Because Presenter Server and  Mind Studio  are deployed on the same server, you can access  Mind Studio  through the browser using the same IP address. 


## Run<a name="section6245151616426"></a>

1.  Run the license plate recognition application.

    On the toolbar of Mind Studio, click  **Run**  and choose  **Run \> Run 'sample-carplaterecognition'**. As shown in  [Figure 12](#fig12953163061713), the executable application is running on the developer board.

    **Figure  12**  Application running<a name="fig12953163061713"></a>  
    

    ![](figures/7c9dd1a0a188f9dc2f5f25e4023f965.png)

2.  Use the URL displayed upon the start of the Presenter Server service to log in to Presenter Server. For details, see  [Start Presenter Server](#li499911453439).

    Wait for Presenter Agent to transmit data to the server. Click  **Refresh**. When there is data, the icon in the  **Status**  column for the corresponding channel changes to green, as shown in  [Figure 13](#fig113691556202312).

    **Figure  13**  Presenter Server page<a name="fig113691556202312"></a>  
    ![](figures/presenter-server-page-29.png "presenter-server-page-29")

    >![](public_sys-resources/icon-note.gif) **NOTE:**   
    >-   For the license plate recognition application, Presenter Server supports a maximum of 10 channels at the same time \(each  _presenter\_view\_app\_name_  parameter corresponds to a channel\).  
    >-   Due to hardware limitations, each channel supports a maximum frame rate of 20 fps. A lower frame rate is automatically used when the network bandwidth is low.  

3.  Click the link \(such as  **video**  in the preceding figure\) in the  **View Name**  column to view the result. The information of the detected license plate is displayed.

## Follow-up Operations<a name="section1092612277429"></a>

-   Stopping the license plate recognition application

    The license plate recognition application is running continually after being executed. To stop it, perform the following operation:

    Click the stop button shown in  [Figure 14](#fig14326454172518).

    **Figure  14**  Stopping the license plate recognition application<a name="fig14326454172518"></a>  
    

    ![](figures/9381c4c3003c7f2cf5479b0464b177f.png)

    [Figure 15](#fig2182182518112)  shows that the license plate recognition application has been stopped.

    **Figure  15**  Stopped license plate recognition application<a name="fig2182182518112"></a>  
    

    ![](figures/186ec128ed22c2f0edfabf73aae63dc.png)

-   Stopping the Presenter Server service

    The Presenter Server service is always in the running state after being started. To stop the Presenter Server service of the license plate recognition application, perform the following operations:

    On the server with  Mind Studio  installed, run the following command as the  Mind Studio  installation user to check the process of the Presenter Server service corresponding to the license plate recognition application:

    **ps -ef | grep presenter | grep carplate\_recognition**

    ```
    ascend@ascend-HP-ProDesk-600-G4-PCI-MT:~/sample-carplaterecognition$ ps -ef | grep presenter | grep carplate_recognition
    ascend    7701  1615  0 14:21 pts/8    00:00:00 python3 presenterserver/presenter_server.py --app carplate_recognition
    ```

    In the preceding information,  _7701_  indicates the process ID of the Presenter Server service corresponding to the license plate recognition application.

    To stop the service, run the following command:

    **kill -9** _7701_

