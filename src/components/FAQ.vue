<template>
    <section id="faq">
        <h2>Frequently Asked Questions</h2>
        <details>
            <summary>
                What risks are involved?
            </summary>
            <p>
                This was whipped together in a couple of hours. It is not well tested and may break your Stremio
                profile. Stremio functionality relies on the existence of certain addons (ie, Cinemeta). It is
                possible that the order of addons is also important to some functionality.
            </p>
            <p>
                There is currently no way to 'reset' your addons to previous configurations or default
                configurations.
            </p>
        </details>
        <details>
            <summary>
                Are my credentials safe?
            </summary>
            <p>
                Yes. We only use your credentials to authenticate with the Stremio API. We do not store them in any way; as soon as you refresh the page they are gone.
            </p>
            <p>
                If you're still in doubt, we highly encourage you to go read the source code. You'll see there's no hidden funny business going on.
            </p>
        </details>
        <details>
            <summary>
                What are the (Web) Developer Tools and how do I open them?
            </summary>
            <p>
                The browser's (Web) Developer Tools are a set of tools which log the information associated with a web
                application, such as network requests and errors. They also let you interact with the loaded web page using
                JavaScript via the Console tab. Most modern browsers have them built in.
            </p>
            <p>
                In most browsers you can open them with <kbd>F12</kbd> (or <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>I</kbd>,
                <kbd>Cmd</kbd>+<kbd>Option</kbd>+<kbd>I</kbd> on macOS), then switch to the <strong>Console</strong> tab,
                ensuring you have the Stremio web app open.
            </p>
        </details>
        <details>
            <summary>
                Can I use this to move Cinemeta catalogs from the top?
            </summary>
            <p>
                Yes! This will allow you to move the Cinemeta provided catalogs (ie, Popular - Series/Movie and Featured -
                Series/Movie) from the top of your catalog list.
            </p>
            <p>
                Do note that the in-built 'Continue watching' catalog cannot be moved from the top.
            </p>
        </details>
    </section>
</template>
