<template>
    <div class="container">
        <div class="row">
            <div v-if="listing" class="col-sm-12">
                <div class="card">
                    <div style="text-align: center;">
                        <img class="card-img-top" :src="listing.image" style="width: 300px; height: auto;">
                    </div>
                    <div class="card-body">
                        <h5 class="card-title">
                            {{listing.title}}
                        </h5>
                        <h6 class="card-subtitle mb-2 ">
                            {{listing.formattedTime}}
                        </h6>
                        <p class="card-text">
                            {{listing.description}}
                        </p>
                    </div>
                    <ul class="list-group list-group-flush">
                        <li class="list-group-item"><i class="fa fa-at"></i> {{listing.user.email}}</li>
                        <li class="list-group-item"><i class="fa fa-phone"></i> {{listing.user.phoneNumber}}</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>
<style>
    .card-body {
        background-color: #0f4471;
        color: #f6f6f6;
    }

    .card-footer {
        background-color: #083358;
        color: #f6f6f6;
    }

    .fa {
        color: #f6f6f6;
    }

    .list-group-item {
        background-color: #083358;
        color: #f6f6f6;
    }

</style>

<script>
    import {
        ListingsService
    } from '../services/listings-service';

    export default {
        name: 'ListingDetails',
        data: function() {
            return {
                'listing': null
            }
        },
        created: function() {
            const listingsService = new ListingsService();
            listingsService.getListing(this.$route.params.id).then(response => {
                this.listing = response.body.data.listing;
                const date = new Date(this.listing.createdAt);
                this.listing.formattedTime = date.toLocaleString();
            });
        }
    }

</script>

<style>
    .blue {
        color: #007bff;
    }

</style>
