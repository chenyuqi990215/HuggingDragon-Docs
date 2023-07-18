####################################
Visualization of Trajectory Recovery
####################################

In this tutorial, we show the process of visualizing trajectory recovery
tasks using pretrained models.

Step 1: Import necessary packages.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: ipython3

    from IPython.display import IFrame
    from huggingdragon.visualizer import TrajRecVisualizer
    import numpy as np

Step 2: Load pretrained model.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this step, we will first download the checkpoint from Google Drive.
Next, the configuration file will be loaded, and the runtime parameters
will be obtained from the YAML config.

.. code:: ipython3

    model = TrajRecVisualizer.from_pretrained('MTrajRec_Porto')
    model


.. parsed-literal::

    Download checkpoint!




.. parsed-literal::

    MTrajRec(
      (encoder): Encoder(
        (pred_out): Linear(in_features=128, out_features=1, bias=True)
        (network): GRU(3, 128)
        (extra): ExtraMLP(
          (fc_out): Linear(in_features=25, out_features=8, bias=True)
        )
        (fc_hid): Linear(in_features=136, out_features=128, bias=True)
      )
      (decoder): DecoderMulti(
        (emb_id): Embedding(12614, 128)
        (tandem_fc): Sequential(
          (0): Linear(in_features=256, out_features=128, bias=True)
          (1): ReLU()
        )
        (attn): Attention(
          (attn): Linear(in_features=256, out_features=128, bias=True)
          (v): Linear(in_features=128, out_features=1, bias=False)
        )
        (rnn): GRU(257, 128)
        (fc_id_out): Linear(in_features=128, out_features=12614, bias=True)
        (fc_rate_out): Linear(in_features=128, out_features=1, bias=True)
        (dropout): Dropout(p=0.1, inplace=False)
      )
    )



Step 3: Obtain the outputs
~~~~~~~~~~~~~~~~~~~~~~~~~~

In this step, we first create a trajectory, and then forward it to the
network to obtain the recovered trajectory.

.. code:: ipython3

    traj = [
        [1372638641, 41.16420900, -8.62301700],
        [1372638761, 41.16493800, -8.62815600],
        [1372638881, 41.16491100, -8.62840800],
        [1372639001, 41.16353400, -8.62766100],
        [1372639121, 41.16274200, -8.62098300],
        [1372639241, 41.16105900, -8.60751900],
        [1372639361, 41.15347200, -8.59973400],
        [1372639481, 41.14691100, -8.59778100],
    ]

.. code:: ipython3

    outputs = TrajRecVisualizer.get_prediction('MTrajRec_Porto', traj, model, time_interval=15)


.. parsed-literal::

    Predict output generated!


Step 4: Visualization
~~~~~~~~~~~~~~~~~~~~~

We use ``folium`` package to visualize the input trajectory as well as
the output trajectory. Orange stars represent the input trajectory,
while the purple line is the output trajectory.

.. code:: ipython3

    TrajRecVisualizer.get_visualization(np.array(traj)[:, 1:], outputs[1:], 'MTrajRec.html')

.. code:: ipython3

    IFrame(src='MTrajRec.html', width=500, height=300)

.. raw:: html

    
    <!DOCTYPE html>
    <html>
    <head>

        <meta http-equiv="content-type" content="text/html; charset=UTF-8" />

            <script>
                L_NO_TOUCH = false;
                L_DISABLE_3D = false;
            </script>

        <style>html, body {width: 100%;height: 100%;margin: 0;padding: 0;}</style>
        <style>#map {position:absolute;top:0;bottom:0;right:0;left:0;}</style>
        <script src="https://cdn.jsdelivr.net/npm/leaflet@1.9.3/dist/leaflet.js"></script>
        <script src="https://code.jquery.com/jquery-1.12.4.min.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.js"></script>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet@1.9.3/dist/leaflet.css"/>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css"/>
        <link rel="stylesheet" href="https://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css"/>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.2.0/css/all.min.css"/>
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.css"/>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/python-visualization/folium/folium/templates/leaflet.awesome.rotate.min.css"/>

                <meta name="viewport" content="width=device-width,
                    initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
                <style>
                    #map_b85ba867c51cfee5604d004e7e5ad723 {
                        position: relative;
                        width: 100.0%;
                        height: 100.0%;
                        left: 0.0%;
                        top: 0.0%;
                    }
                    .leaflet-container { font-size: 1rem; }
                </style>

        <script src="https://cdn.jsdelivr.net/gh/marslan390/BeautifyMarker/leaflet-beautify-marker-icon.min.js"></script>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/marslan390/BeautifyMarker/leaflet-beautify-marker-icon.min.css"/>
    </head>
    <body>


                <div class="folium-map" id="map_b85ba867c51cfee5604d004e7e5ad723" ></div>

    </body>
    <script>


                var map_b85ba867c51cfee5604d004e7e5ad723 = L.map(
                    "map_b85ba867c51cfee5604d004e7e5ad723",
                    {
                        center: [41.1572655, -8.6036265],
                        crs: L.CRS.EPSG3857,
                        zoom: 14,
                        zoomControl: true,
                        preferCanvas: false,
                    }
                );





                var tile_layer_68d9c69dfaa784e68c1dfa046f711b01 = L.tileLayer(
                    "https://{s}.basemaps.cartocdn.com/light_nolabels/{z}/{x}/{y}{r}.png",
                    {"attribution": "\u0026copy; \u003ca href=\"https://www.openstreetmap.org/copyright\"\u003eOpenStreetMap\u003c/a\u003e contributors \u0026copy; \u003ca href=\"https://carto.com/attributions\"\u003eCARTO\u003c/a\u003e", "detectRetina": false, "maxNativeZoom": 18, "maxZoom": 18, "minZoom": 0, "noWrap": false, "opacity": 1, "subdomains": "abc", "tms": false}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var marker_7cc8d32eaef2747ec4d7a61d95acbe92 = L.marker(
                    [41.164209, -8.623017],
                    {}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var beautify_icon_c0c663f582ea5b43b3f6f045aa67602d = new L.BeautifyIcon.icon(
                    {"backgroundColor": "transparent", "borderColor": "transparent", "borderWidth": 3, "icon": "star", "innerIconStyle": "color:#9E189D;font-size:25px;", "isAlphaNumericIcon": false, "spin": false, "textColor": "#000"}
                )
                marker_7cc8d32eaef2747ec4d7a61d95acbe92.setIcon(beautify_icon_c0c663f582ea5b43b3f6f045aa67602d);


                var marker_d2e9bf68588af7769ce1a093e2d40c8a = L.marker(
                    [41.164938, -8.628156],
                    {}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var beautify_icon_002a389f77d043a838635748fff8e150 = new L.BeautifyIcon.icon(
                    {"backgroundColor": "transparent", "borderColor": "transparent", "borderWidth": 3, "icon": "star", "innerIconStyle": "color:#9E189D;font-size:25px;", "isAlphaNumericIcon": false, "spin": false, "textColor": "#000"}
                )
                marker_d2e9bf68588af7769ce1a093e2d40c8a.setIcon(beautify_icon_002a389f77d043a838635748fff8e150);


                var marker_335ba20451c151fd2a5481682be4a0f2 = L.marker(
                    [41.164911, -8.628408],
                    {}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var beautify_icon_b01486cbb695355b6d69ec085f9caf20 = new L.BeautifyIcon.icon(
                    {"backgroundColor": "transparent", "borderColor": "transparent", "borderWidth": 3, "icon": "star", "innerIconStyle": "color:#9E189D;font-size:25px;", "isAlphaNumericIcon": false, "spin": false, "textColor": "#000"}
                )
                marker_335ba20451c151fd2a5481682be4a0f2.setIcon(beautify_icon_b01486cbb695355b6d69ec085f9caf20);


                var marker_e560084b19e535966cd0cb62eb575ce1 = L.marker(
                    [41.163534, -8.627661],
                    {}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var beautify_icon_fc343a6cc2a428362b6710ad92acccf2 = new L.BeautifyIcon.icon(
                    {"backgroundColor": "transparent", "borderColor": "transparent", "borderWidth": 3, "icon": "star", "innerIconStyle": "color:#9E189D;font-size:25px;", "isAlphaNumericIcon": false, "spin": false, "textColor": "#000"}
                )
                marker_e560084b19e535966cd0cb62eb575ce1.setIcon(beautify_icon_fc343a6cc2a428362b6710ad92acccf2);


                var marker_21eb9adf65ffaa61beee66f9bf0ce1d5 = L.marker(
                    [41.162742, -8.620983],
                    {}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var beautify_icon_ad091e12eff70497c721773d2ca10602 = new L.BeautifyIcon.icon(
                    {"backgroundColor": "transparent", "borderColor": "transparent", "borderWidth": 3, "icon": "star", "innerIconStyle": "color:#9E189D;font-size:25px;", "isAlphaNumericIcon": false, "spin": false, "textColor": "#000"}
                )
                marker_21eb9adf65ffaa61beee66f9bf0ce1d5.setIcon(beautify_icon_ad091e12eff70497c721773d2ca10602);


                var marker_b117e50aac0d61d299c89cfbb5bfb486 = L.marker(
                    [41.161059, -8.607519],
                    {}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var beautify_icon_b2583ed265b6ec7a88f0fee5e5ccec73 = new L.BeautifyIcon.icon(
                    {"backgroundColor": "transparent", "borderColor": "transparent", "borderWidth": 3, "icon": "star", "innerIconStyle": "color:#9E189D;font-size:25px;", "isAlphaNumericIcon": false, "spin": false, "textColor": "#000"}
                )
                marker_b117e50aac0d61d299c89cfbb5bfb486.setIcon(beautify_icon_b2583ed265b6ec7a88f0fee5e5ccec73);


                var marker_236787b27f0d22bd74771d023f678912 = L.marker(
                    [41.153472, -8.599734],
                    {}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var beautify_icon_15cbcc3887414e312211c7532e956dd3 = new L.BeautifyIcon.icon(
                    {"backgroundColor": "transparent", "borderColor": "transparent", "borderWidth": 3, "icon": "star", "innerIconStyle": "color:#9E189D;font-size:25px;", "isAlphaNumericIcon": false, "spin": false, "textColor": "#000"}
                )
                marker_236787b27f0d22bd74771d023f678912.setIcon(beautify_icon_15cbcc3887414e312211c7532e956dd3);


                var marker_4e3eb2b2bac363d1412efb960ca9bbf3 = L.marker(
                    [41.146911, -8.597781],
                    {}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);


                var beautify_icon_f251c4bdf9d1831ed4ebd10e6cb46634 = new L.BeautifyIcon.icon(
                    {"backgroundColor": "transparent", "borderColor": "transparent", "borderWidth": 3, "icon": "star", "innerIconStyle": "color:#9E189D;font-size:25px;", "isAlphaNumericIcon": false, "spin": false, "textColor": "#000"}
                )
                marker_4e3eb2b2bac363d1412efb960ca9bbf3.setIcon(beautify_icon_f251c4bdf9d1831ed4ebd10e6cb46634);


                var poly_line_f998aa01b1b5efa8133692822fe1b58a = L.polyline(
                    [[41.165523529052734, -8.627556800842285], [41.173519134521484, -8.613117218017578], [41.173492431640625, -8.61310863494873], [41.17350387573242, -8.613113403320312], [41.17347717285156, -8.613103866577148], [41.173458099365234, -8.613097190856934], [41.1734504699707, -8.6130952835083], [41.174686431884766, -8.616816520690918], [41.1746826171875, -8.61691665649414], [41.174686431884766, -8.616864204406738], [41.1746826171875, -8.616867065429688], [41.174678802490234, -8.616929054260254], [41.174678802490234, -8.616927146911621], [41.171688079833984, -8.633777618408203], [41.168052673339844, -8.625385284423828], [41.168060302734375, -8.625387191772461], [41.16493225097656, -8.628847122192383], [41.16736602783203, -8.625239372253418], [41.16737747192383, -8.625242233276367], [41.16736602783203, -8.625239372253418], [41.16739273071289, -8.625245094299316], [41.16739273071289, -8.625245094299316], [41.16511154174805, -8.6248779296875], [41.16501998901367, -8.624870300292969], [41.16356658935547, -8.628214836120605], [41.16356658935547, -8.628207206726074], [41.1635627746582, -8.62814998626709], [41.163421630859375, -8.625853538513184], [41.16340637207031, -8.62558650970459], [41.16340255737305, -8.62551498413086], [41.16340637207031, -8.62557315826416], [41.162960052490234, -8.62258529663086], [41.16276168823242, -8.621122360229492], [41.1629524230957, -8.622543334960938], [41.16276168823242, -8.621137619018555], [41.162601470947266, -8.619219779968262], [41.16244125366211, -8.617321014404297], [41.16218185424805, -8.615082740783691], [41.161991119384766, -8.613555908203125], [41.161991119384766, -8.613550186157227], [41.16116714477539, -8.608113288879395], [41.16081237792969, -8.606307983398438], [41.16080093383789, -8.606241226196289], [41.16010665893555, -8.603556632995605], [41.15962219238281, -8.60176944732666], [41.159610748291016, -8.60172176361084], [41.15898895263672, -8.599366188049316], [41.15898513793945, -8.599360466003418], [41.15382385253906, -8.599617004394531], [41.1556282043457, -8.599272727966309], [41.15385055541992, -8.599611282348633], [41.15239715576172, -8.59988021850586], [41.14990234375, -8.600356101989746], [41.14871597290039, -8.59874153137207], [41.148704528808594, -8.598736763000488], [41.1486930847168, -8.598729133605957], [41.14723205566406, -8.597770690917969]],
                    {"bubblingMouseEvents": true, "color": "#F46F44", "dashArray": null, "dashOffset": null, "fill": false, "fillColor": "#F46F44", "fillOpacity": 0.2, "fillRule": "evenodd", "lineCap": "round", "lineJoin": "round", "noClip": false, "opacity": 0.8, "smoothFactor": 1.0, "stroke": true, "weight": 5}
                ).addTo(map_b85ba867c51cfee5604d004e7e5ad723);

    </script>
    </html>



