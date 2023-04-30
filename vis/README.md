# Graph improvements

<p float="left">
  <img src="https://github.com/TheFox9711/MLPNS_LVolpi/blob/main/vis/prima.jpg" width="49%" height="49%"/>
  <img src="https://github.com/TheFox9711/MLPNS_LVolpi/blob/main/vis/dopo.jpg" width="49%" height="49%"/>
</p>

## Improvements (left: before, right: after):
- Use of more readable ticks and labels for the axes (multiples and submultiples of Ohm and Ampère, powers instead of fraction...)
- Decreased the size of datapoints, so we can read their values more easily, and plotted them over the fitting line
- Use of a complete box around the graph (not very useful but it makes it better looking, at least for me)
- Changed the style of grid lines from solid to dashed, here we are interested in the trend of the datas (in particular we want to verify that the inverse of the current $I^{-1}$ and the resistance $R$ are linearly correlated), we don't really need to read their exact values so we hide unnecessary lines and focus only on the fitting line and the datas themselves. Nevertheless we use a dahsed grid in the case someone wants to get an idea of the values we measured.

## Code
For the left graph:
```matlab
% Plot
errorbar(x, y, delta, 'o', 'MarkerSize', 10);

hold on
xlim([0 max(x)+min(x)]);

% Fit
dom = xlim();
plot(dom, m * dom + q);

% Labels
xlabel('R (Ω)');
ylabel('1/I (A^{-1})');

% Grid
grid on
box off
```

For the right graph:
```matlab
% Plot
new_x = x / 1e3; new_y = y / 1e3;
errorbar(new_x, new_y, delta / 1e3, '.', 'MarkerSize', 12);

hold on
xlim([0 max(new_x)+min(new_x)]);

% Fit
dom = xlim();
plot(dom, m * dom + q/1e3);

% Labels
xlabel('$R\;\;$ [k$\Omega$]', 'Interpreter', 'latex');
ylabel('$I^{-1}\;\;$ [mA$^{-1}$]', 'Interpreter', 'latex');

% Axes
ax = gca;
ax.FontSize = 12;
set(ax, 'fontname', 'times');
set(ax, 'Children', flip(get(ax, 'Children')));

% Grid
grid on
set(ax, 'GridLineStyle', '--')
```
