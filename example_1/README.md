# Example 1: Autonomous cars

Paste the following theory in the theory section of the __Arg2pIDE__:

```
r1 : on_road(V),
    traffic_light(V, red) => o(stop(V)).
r2 : on_road(V),
    traffic_light(V,green) => p(-stop(V)).
r3 : on_road(V), authorised_vehicle(V),
    acoustic_signals(V, on),
    light_signals(V, on) => emergency(V).
r4 : on_road(V), emergency(V),
    traffic_light(V, red) => p(-stop(V)).
r5 : on_road(V), emergency(V1),
    prolog(V \== V1),
    traffic_light(V, green) => o(stop(V)).

sup(r4, r1).
sup(r5, r2).

f0 :-> authorised_vehicle(ambulance).
f1 :-> on_road(car).
f2 :-> on_road(ambulance).
f3 :-> on_road(pedestrian).
f4 :=> acoustic_signals(ambulance, on).
f5 :=> light_signals(ambulance, on).
f6 :=> traffic_light(ambulance, red).
f7 :=> traffic_light(car, red).
f8 :=> traffic_light(pedestrian, green).
```

This should be the result

![Theory](../images/example_1_paste.png)

Now open the __Arg Flags__ tab and configure the engine as follows:

![Flags](../images/base_flags.png)

By using these settings, we are requiring the evaluation of the thery according to __grounded__ semantic and using the __last/elitist__ principle for handling preferences. We also disable the __rebut restriction__.

To require the evalution use the predicate `buildLabelSets`. Just put it in the query section (__?-__) and press the __Solve__ button.

![Run](../images/buildLabelSets.png)

When the evaluation is complete, you shold see the following result in the __Solutions__ tab:

![Theory](../images/ok_result.png)

You can now explore the result under the __Graph__ tab. There you can find the resulting argumentation graph coloured according to the computed labelling (red for __OUT__ arguments, green for __IN__ arguments, gray for __UND__ arguments).

![Theory](../images/example_1_graph_tab.png)

You can now play with the flags in the __Arg Flags__ tab to customise the evaluation to your needs and explore all the available solutions. You can find a description of the flags and their behaviour in the official [wiki](https://pika-lab.gitlab.io/argumentation/arg2p-kt/wiki/predicate/).