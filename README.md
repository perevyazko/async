#python 3.6
# async 

start = time()

async def spider(site_name):
    for page in range(1, 4):

        await asyncio.sleep(1)
        if site_name == "Forum":
            print(site_name, page)


spider("Blog")
spider("News")
spider("Forum")

spiders = [
    asyncio.ensure_future(spider("Blog")),
    asyncio.ensure_future(spider("News")),
    asyncio.ensure_future(spider("Forum"))
]

event_loop = asyncio.get_event_loop()
now = event_loop.time()
event_loop.call_soon(loader, "url 1")
event_loop.call_at(now + 2, loader, "url 2")
event_loop.run_until_complete(asyncio.gather(*spiders))
event_loop.close()

print("{:.2F}".format(time() - start))
