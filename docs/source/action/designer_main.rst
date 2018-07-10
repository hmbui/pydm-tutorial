.. _Main:

Main Screen
===========

.. important::

    **Check-list:**

    * Make sure that you have your :ref:`Environment <Environment>` properly configured.
    * That your :ref:`VirtualMachine` is up and ready.
    * That the :ref:`Python environment <PythonEnv>` is set.
    * That all :ref:`three IOCs <IOCS>` are running.


This will be the main point of our Beam Positioning application and will group all the other
components of this tutorial.

The finished result will look like this:

.. figure:: /_static/action/main/main.png
   :scale: 75 %
   :align: center
   :alt: Expert Motor Screen

   Main Screen for Beam Positioning Application


* **Step 1.**

  Let's start by opening the :ref:`Qt Designer <Designer>`
  and creating a new ``Widget``.

  .. figure:: /_static/action/new_widget.gif
     :scale: 100 %
     :align: center

  Save this file as ``main.ui``.

  .. warning::
     For this tutorial it is important to use this file name, as it will be referenced
     at the other sections. If you change it please remember to also change at the
     next steps when referenced.

* **Step 2.**

  With the new form available, let's add a ``QVBoxLayout`` widget and make
  it fill the whole form. Let's select ``Layout Vertically`` for the Form.

  .. figure:: /_static/action/inline/inline_layout.gif
     :scale: 100 %
     :align: center

* **Step 3.**

  Now that we have a layout, let's take a look at the widgets on this screen:

  .. figure:: /_static/action/main/widgets.png
     :scale: 70 %
     :align: center

  * **Step 3.1.**

    The first ``QLabel`` will be the title of our screen:

    #. Drag and drop a ``QLabel`` into the previously added ``QVBoxLayout``.
    #. Set the ``text`` property of this label to: ``Beam Alignment``.
    #. In order to make the label look better as a title, add the following to the ``stylesheet`` property:

       .. code-block:: css

            QLabel {
                qproperty-alignment: AlignCenter;
                border: 1px solid #FF17365D;
                border-top-left-radius: 15px;
                border-top-right-radius: 15px;
                background-color: #FF17365D;
                padding: 5px 0px;
                color: rgb(255, 255, 255);
                max-height: 25px;
                font-size: 14px;
            }

  * **Step 3.2.**

    The second widget that we will add is a ``PyDMImageView``, which will display
    the image coming from our camera:

    #. Drag and drop a ``PyDMImageView`` into the previously added ``QVBoxLayout`` under
       the ``QLabel`` that was added at **Step 3.1**.
    #. Set the ``objectName`` property of this widget to ``imageView``.

        .. important::

            It is very important to set the ``objectName`` property of widgets as instructed, using Qt Designer, so that
            you can refer to them by the Python code you are to add in the later steps.

    #. Set the ``imageChannel`` property to ``ca://13SIM1:image1:ArrayData``.
    #. Set the ``widthChannel`` property to ``ca://13SIM1:image1:ArraySize1_RBV``.
    #. Set the ``readingOrder`` property to ``Clike``.
    #. Set the ``maxRedrawRate`` property to ``30`` so we can update the image at
       30 Hz.

  * **Step 3.3.**

    The third widget that we will add is a ``QVBoxLayout``, which will be the
    placeholder for the controls area of the screen:

    #. Drag and drop a ``QVBoxLayout`` into the previously added ``QVBoxLayout`` under
       the ``PyDMImageView`` that was added at **Step 3.2**.

  * **Step 3.4.**

    The fourth widget that we will add is a ``QLabel``, which will updated with
    the result of the calculation of beam position at the next section (:ref:`LittleCode`):

    #. Drag and drop a ``QLabel`` into ``QVBoxLayout`` that was added at
       **Step 3.3**. Make sure you drop this ``QLabel`` widget into the ``QVBoxLayout`` at **Step 3.3** and not the
       ``QVBoxLayout`` added at **Step 3.2**.
    #. Set the ``objectName`` property of this widget to ``lbl_blobs``.

       .. important::

            It is very important to set the ``objectName`` property of widgets as instructed, using Qt Designer, so that
            you can refer to them by the Python code you are to add in the later steps.

    #. Set the ``text`` property to empty so this label will only show information
       when we write to it using the code later on.

  * **Step 3.5.**

    The fifth widget that we will add is another ``QLabel``, which will the title of our controls area:

    #. Drag and drop a ``QLabel`` under the QLabel added at **Step 3.4**. The new label should be directly contained by
       the ``QVBoxLayout`` that was added at **Step 3.3**.
    #. Set the ``text`` property of this label to: ``Controls``.
    #. In order to make the label look better as a title, add the following to the ``stylesheet`` property:

       .. code-block:: css

            QLabel {
                qproperty-alignment: AlignCenter;
                border: 1px solid #FF17365D;
                border-top-left-radius: 15px;
                border-top-right-radius: 15px;
                background-color: #FF17365D;
                padding: 5px 0px;
                color: rgb(255, 255, 255);
                max-height: 25px;
                font-size: 14px;
            }

  * **Step 3.6.**

    The sixth widget that we will add is a ``QFrame``, which will be the container
    for our two motors ``Embedded Displays``:

    #. Drag and drop a ``QFrame`` under the QLabel added at **Step 3.5**.
    #. Set the ``frameShape`` property to ``StyledPanel``.
    #. Set the ``frameShadow`` property to ``Raised``
    #. Set the ``stylesheet`` property to:

       .. code-block:: css

            QFrame#frame{
                border: 1px solid #FF17365D;
                border-bottom-left-radius: 15px;
                border-bottom-right-radius: 15px;
            }

  * **Step 3.7.**

    The seventh widget that we will add is a ``PyDMEmbeddedDisplay``, which will
    display the ``inline_motor.ui`` with information for our first motor axis:

    #. Drag and drop a ``PyDMEmbeddedDisplay`` into the ``QFrame`` added at **Step 3.6**.
    #. Right-click at the ``QFrame`` from **Step 3.6** and select ``Layout >> Layout Vertically``.
    #. Set the embedded display's ``macros`` property to ``{"MOTOR":"IOC:m1"}``.
    #. Set the embedded display's ``filename`` property to ``inline_motor.ui``.

  * **Step 3.8.**

    The eighth widget that we will add is a ``PyDMEmbeddedDisplay``, which will
    display the ``inline_motor.ui`` with information for our second motor axis:

    #. Drag and drop a ``PyDMEmbeddedDisplay`` into the ``QFrame`` added at **Step 3.7**.
    #. Set the embedded display's ``macros`` property to ``{"MOTOR":"IOC:m2"}``.
    #. Set the embedded display's ``filename`` property to ``inline_motor.ui``.

  * **Step 3.9.**

    Finally, the ninth widget that we will add is a ``PyDMRelatedDisplayButton``, which will
    open the ``All Motors`` screen that will be developed :ref:`later <PurePython>`:

    #. Drag and drop a ``PyDMRelatedDisplayButton`` into the ``QVBoxLayout`` added at **Step 2**.
    #. Set the ``text`` property of this label to ``View All Monitors``.
    #. Set the ``displayFilename`` property to ``all_motors.py``.
    #. Remove the mark at the ``openInNewWindow`` property.

  * **Step 3.10.**

    Once all the widgets are added to the form, it is now time to adjust the layouts
    and make sure that all is well positioned and behaving nicely.

    #. Using the ``Object Inspector`` at the top-right corner of the Qt Designer
       window, select the ``frame`` object and set the properties according
       to the table below:

       ==================================  ==================
       Property                            Value
       ==================================  ==================
       layoutLeftMargin                    0
       layoutTopMargin                     0
       layoutRightMargin                   0
       layoutBottomMargin                  0
       layoutSpacing                       0
       ==================================  ==================

    #. Continuing with the ``Object Inspector``, select the ``vertical layout``
       object right before the ``frame`` and set the properties according to the
       table below:

       ==================================  ==================
       Property                            Value
       ==================================  ==================
       layoutSpacing                       0
       ==================================  ==================

    #. Still with the ``Object Inspector``, now select the top most ``verticalLayout``
       object set the properties according to the table below:

       ==================================  ==================
       Property                            Value
       ==================================  ==================
       layoutSpacing                       0
       ==================================  ==================

    The end result will be something like this:

    .. figure:: /_static/action/main/main_all_widgets_ok.png
       :scale: 100 %
       :align: center

* **Step 4.**

  Save this file as ``main.ui`` again if necessary.

* **Step 5.**

  Test the Expert Motor Screen:

  .. code-block:: bash

     pydm main.ui

  .. figure:: /_static/action/main/main.png
     :scale: 75 %
     :align: center
     :alt: Main Application Screen

.. note::
    You can download this file using :download:`this link </_static/code/main.ui>`.

