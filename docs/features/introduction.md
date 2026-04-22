# Introduction OGC API - Features

!!! abstract "Learning goals"

    After completing this section:

    - You know which parts OGC API (- Features) consists of and what those parts do;
    - You know which parts PDOK has implemented;
    - You can use the PDOK OGC APIs landing page:
        - You can view data examples via the landing page;
        - You can find and use OGC API - Features URLs;
    - You can query feature data from the command line;
    - You can compose an API GET request with bbox, pagination, CRS, and feature-id;
    - You know how a web map works;
    - You can show OGC API - Features on a web map and let users interact with it.

In this section, we explore OGC API - Features, query it from the command line, and build an interactive map.

OGC API - Features publishes feature data (vector data) as JSON. If you need full data or subsets of data and users should interact with it, OGC API - Features is the right choice. Data completeness and filtering capabilities are key.

First, using the API landing page, you learn what is possible and get a preview of data. Then we cover querying the API via command line. Finally, you build your own web map with OGC API - Features so end users can use geodata interactively.

!!! info "You will work with:"

    - Web browser
    - Command line
        - curl
    - Code editor
    - MapLibre (JavaScript)
