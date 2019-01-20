# Concurrent Atomic Design Systems

The use of concurrent atomic design systems, or CADS, has been added into Particle as of v10.2. Developers can now create multiple apps using completely separate design systems within Particle with only minor configuration changes to the new app's config file.

## Adding New CADS

1. Inside the `source` directory, create a copy of the `default` folder with its own unique name.
1. Open the `apps` directory in your project root and create a copy of the app folder you want to work with.
1. In your new app's folder, open the `config.js` file.
1. Find the line that contains `APP_DESIGN_SYSTEM` and change the target directory, `default`, to the name of your new design system's folder.
