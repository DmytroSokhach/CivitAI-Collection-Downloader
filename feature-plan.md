1. Article on Civit Rest api: https://huggingface.co/blog/hlky/web-scraping-102

Collection filtered only by ComfyUI and Illustrous and withMeta
https://civitai.com/collections/6640851?baseModels=Illustrious&withMeta=true&tools=86

https://civitai.com/api/trpc/image.getInfinite?input=%7B%22json%22%3A%7B%22baseModels%22%3A%5B%22Illustrious%22%5D%2C%22collectionId%22%3A6640851%2C%22tools%22%3A%5B86%5D%2C%22withMeta%22%3Atrue%2C%22period%22%3A%22AllTime%22%2C%22sort%22%3A%22Newest%22%2C%22browsingLevel%22%3A31%2C%22include%22%3A%5B%22cosmetics%22%5D%2C%22excludedTagIds%22%3A%5B306619%2C5351%2C154326%2C161829%2C163032%2C5188%5D%2C%22disablePoi%22%3Atrue%2C%22disableMinor%22%3Atrue%2C%22cursor%22%3Anull%2C%22authed%22%3Atrue%7D%2C%22meta%22%3A%7B%22values%22%3A%7B%22cursor%22%3A%5B%22undefined%22%5D%7D%7D%7D

'https://civitai.com/api/trpc/image.getInfinite?input={"json":{"baseModels":["Illustrious"],"collectionId":6640851,"tools":[86],"withMeta":true,"period":"AllTime","sort":"Newest","browsingLevel":31,"include":["cosmetics"],"excludedTagIds":[306619,5351,154326,161829,163032,5188],"disablePoi":true,"disableMinor":true,"cursor":null,"authed":true},"meta":{"values":{"cursor":["undefined"]}}}'


2. Try other solutions:
    1. Simple image grabber (has download tracking support): https://github.com/Confuzu/CivitAI_Image_grabber
        a. Also seems to have tag search!
    2. Powerful tool: https://github.com/mikf/gallery-dl
        Seems doesn't download "collections"