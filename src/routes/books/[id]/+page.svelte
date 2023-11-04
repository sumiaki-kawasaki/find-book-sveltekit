<script lang="ts">
  import { page } from '$app/stores';
  import Spinner from '$lib/Spinner.svelte';
  import BookInfo from '$lib/BookInfo.svelte';
  import type { Readable } from 'svelte/store';
  import type { BookItem } from '$lib/repositories/book';
  import RepositoryFactory, { BOOK } from '$lib/repositories/RepositoryFactory';
  import { find, books } from '$lib/store/book';
  const BookRepository = RepositoryFactory[BOOK];

  let book: Readable<BookItem>;
  let promise: Promise<void>;

  const findById = async (id: string) => {
    const book = await BookRepository.find(id);
    books.add([book]);
  };

  // console.log($page);
  // console.log(`id:${$page.params.id}`);

  book = find($page.params.id);
  if (!$book) {
    promise = findById($page.params.id);
  }
</script>

<div>
  {#await promise}
    <div class="flex justify-center">
      <Spinner />
    </div>
  {:then}
    <BookInfo book={$book} />
  {:catch e}
    <span class="text-red-600 text-sm">
      {e.message}
    </span>
  {/await}
</div>
