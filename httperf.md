httperf --hog --server=www.site.com.br --wsess=10000,5,3 --rate 25 --timeout 5
# 1000 req/min
httperf --hog --server=www.site.com.br --num-conns 100000 --rate 17 --timeout 5
# 2000 req/min
httperf --hog --server=www.site.com.br --num-conns 100000 --rate 35 --timeout 5
# 6000 req/min
httperf --hog --server=www.site.com.br --num-conns 100000 --rate 100 --timeout 5
# 11000 req/min
httperf --hog --server=www.site.com.br --num-conns 100000 --rate 185 --timeout 5
# 32000 req/min
httperf --hog --server=www.site.com.br --num-conns 1000000 --rate 535 --timeout 5
# 52000 req/min
httperf --hog --server=www.site.com.br --num-conns 1000000 --rate 870 --timeout 5
# 1200 req/min com uri
httperf --hog --server=www.site.com.br --uri=/?no_cache=1 --num-conns 1000000 --rate 20 --timeout 5