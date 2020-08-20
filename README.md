# vue-swr

vue-SWR is a great to help make it easier to fetch remote data with hooks. It is based on the stale-while-revalidate RFC, which in simple terms says to show stale (old) data while you are fetching a new version of the data. The idea is that it is better to show something old if you have it rather than a blank screen.


The useSWR hook requires two things to make it work:
* A key: This is a little vague, but think it if as something that uniquely identifies the data you want to fetch... which for a RESTful API endpoint can be the URL.
* A fetcher: This is a function who will do the work of making the actual API request. In our case we'll be using fetch, but you could use axios if you prefer. Its only requirement is that it returns a promise which resolves the data you are fetching.

Example code:
    
<script>
import { fetcher } from '../utils/fetcher';
import { useSwrCache, STATE } from '../composables/swr-cache';

export default {
  name: 'component',
  setup() {
    const {
      data: user,
      error,
      state,
    } = useSwrCache('https://blablavla/1', fetcher);

    return {
      STATE,
      error,
      state,
      user,
    };
  },
};
</script>
